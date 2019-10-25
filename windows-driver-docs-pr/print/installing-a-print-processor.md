---
title: 安装打印处理器
description: 安装打印处理器
ms.assetid: 4e9e1148-16a3-42f6-a262-1eef014636d0
keywords:
- 打印处理器 WDK，安装
- 安装打印处理器 WDK
- 打印队列-WDK，打印处理器安装
- 将打印处理器与打印队列 WDK 关联
- 打印处理器 WDK，与打印队列关联
- 打印队列 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 024fadaef3fef6d144eec8ce8fe2e73affad7f33
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843626"
---
# <a name="installing-a-print-processor"></a>安装打印处理器





若要安装打印处理器，安装应用程序必须调用后台处理程序的**AddPrintProcessor**函数。 若要将打印处理器与打印队列相关联，请在 PrintProcessor 条目中列出 INF 文件中的文件名。 对于打印处理器要关联到的每个打印队列，都必须包含此项。 有关详细信息，请参阅[打印机 INF 文件](printer-inf-files.md)。

当安装应用程序调用后台处理程序的**interactivesession.addprinter**函数时，使用打印机\_信息\_2 结构作为输入参数，它将打印处理器名称（从 INF 文件获取）指定为结构成员。 （Microsoft Windows SDK 文档中介绍了**AddPrintProcessor**和**INTERACTIVESESSION.ADDPRINTER**函数以及打印机\_信息\_2 结构。）

### <a name="associating-a-print-processor-with-a-pnp-installed-print-queue"></a>将打印处理器与 PnP 安装的打印队列关联

如果即插即用（PnP）管理器在运行 Windows 2000 或 Windows XP 的系统上检测并安装打印队列，并且用于安装打印队列的 INF 文件包含除默认 Windows 打印处理器以外的 PrintProcessor 条目，请 WinPrint，打印处理器不会与打印队列关联。 但会安装打印处理器。 （请注意，如果您使用 "添加打印机向导" 安装打印队列，打印处理器将与打印队列正确关联。 另请注意，Microsoft Windows Server 2003 和更高版本中的 PnP 管理器将打印处理器正确关联到打印队列。）

若要在 Windows 2000 和 Windows XP 上将打印处理器与即插即用安装的打印队列相关联，请在打印机接口 DLL 的[**DrvPrinterEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent)函数中包括打印机\_事件\_INITIALIZE case。 对于 Microsoft Windows Server 2003 及更高版本，无需在**DrvPrinterEvent**函数中添加打印机\_事件\_INITIALIZE case。

下面的代码示例将打印机\_信息\_2 结构的**pPrintProcessor**成员设置为打印处理器的名称，然后调用**SetPrinter**函数（在 Windows SDK 文档中进行了描述）来更新打印机的设置。 请注意， *gszPrintProc*中打印处理器的名称必须与 INF 文件中 PrintProcessor 条目的名称相同。

```cpp
BOOL
DrvPrinterEvent(
               LPWSTR  pPrinterName,
               INT     Event,
               DWORD   Flags,
               LPARAM  lParam
               )

{
  PRINTER_DEFAULTS  PrinterDef = {NULL, NULL, PRINTER_ALL_ACCESS};
  HANDLE            hPrinter;
  LPPRINTER_INFO_2  pInfo = NULL;
  DWORD             cbNeeded;
  TCHAR             gszPrintProc[] = TEXT("<Print processor name>");
  BOOL              bRet = TRUE;

  switch (Event)
  {
    case PRINTER_EVENT_INITIALIZE:
      if (OpenPrinter(pPrinterName, &hPrinter, &PrinterDef))
      {
        if ( !GetPrinter( hPrinter, 2, (LPBYTE) pInfo, 0, &cbNeeded ) &&
           (GetLastError() != ERROR_INSUFFICIENT_BUFFER) )
        {
          bRet = FALSE;
        }
        if (bRet == TRUE)
        {
          pInfo = (LPPRINTER_INFO_2) LocalAlloc(LPTR, cbNeeded);
          bRet = pInfo ? TRUE : FALSE;
        }
        if (bRet == TRUE)
        {
          if (GetPrinter(hPrinter, 2, (LPBYTE) pInfo, cbNeeded, &cbNeeded))
          {
            pInfo->pPrintProcessor = gszPrintProc;
            SetPrinter(hPrinter, 2, (LPBYTE) pInfo, 0);
          }
          else 
          {
            bRet = FALSE;
          }
          if (pInfo)
          {
            LocalFree(pInfo);
          }
        }
        ClosePrinter(hPrinter);
      }
      else  // OpenPrinter failed
      {
        bRet = FALSE;
      }
    break;
    // cases for other events

    default:
      break;
  }  // end switch
  return bRet;
}
```

### <a href="" id="associating-a-print-processor-with-a-print-queue-during-printer-driver"></a>在打印机驱动程序升级过程中将打印处理器与打印队列关联

更新打印机驱动程序时，不会更改更新的打印队列的打印处理器。 如果新的打印机驱动程序需要特定的打印处理器，则打印机接口 DLL 的[**DrvUpgradePrinter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvupgradeprinter)函数必须将打印机的**pPrintProcessor**成员设置\_信息\_2 结构设置为新打印的名称双核处理器. 出现这种情况后，此函数将调用**SetPrinter**来更新打印机的设置。 后台处理程序为每台打印机调用一次**DrvUpgradePrinter**函数，这可确保使用该驱动程序的所有打印机也使用所需的打印处理器。 下面的代码示例演示了这些要点。

```cpp
BOOL
DrvUpgradePrinter(
                 DWORD   Level,
                 LPBYTE  pDriverUpgradeInfo
                 )
{
  HANDLE                  hPrinter;
  PRINTER_DEFAULTS        PrinterDef = {NULL, NULL, PRINTER_ALL_ACCESS};
 PDRIVER_UPGRADE_INFO_2  pDUI2;
  LPPRINTER_INFO_2        pInfo = NULL;
 DWORD                   cbNeeded;
  TCHAR                   gszPrintProc[]   = TEXT("<Print processor name>");
  TCHAR                   gszPrintDriver[] = TEXT("<Printer driver name>");
  BOOL                    bRet = TRUE;

  if ((Level == 2)                                            &&
      (pDUI2 = (PDRIVER_UPGRADE_INFO_2)pDriverUpgradeInfo)    &&
      (OpenPrinter(pDUI2->pPrinterName, &hPrinter, &PrinterDef)))
  {
    if ( !GetPrinter( hPrinter, 2, (LPBYTE) pInfo, 0, &cbNeeded )  &&
         (GetLastError() != ERROR_INSUFFICIENT_BUFFER) )
    {
       bRet = FALSE;
    }
    if (bRet == TRUE)
    {
      pInfo = (LPPRINTER_INFO_2) LocalAlloc(LPTR, cbNeeded);
      bRet = pInfo ? TRUE : FALSE;
    }
    if (bRet == TRUE)
    {
      if (GetPrinter(hPrinter, 2, (LPBYTE) pInfo, cbNeeded, &cbNeeded))
      {
      //
      // This function is called for every printer queue that uses a driver
      // for which one or more files were updated. However, we only want to
      // update the printer queue's "driver" by a particular driver.
      //
      if ( !lstrcmpi(pInfo->pDriverName, gszPrintDriver) )
      {
        pInfo->pPrintProcessor =  gszPrintProc;
        SetPrinter(hPrinter, 2, (LPBYTE) pInfo, 0);
      }
    else  // GetPrinter 
    {
      bRet = FALSE;
    }
    if (pInfo)
    {
      LocalFree(pInfo);
    }
    ClosePrinter(hPrinter);
  }
  else  // Level != 2 or pDUI2 == NULL or OpenPrinter failed
  {
    bRet = FALSE;
  }
  return bRet;
}
```

 

 




