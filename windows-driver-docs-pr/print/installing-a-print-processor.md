---
title: 安装打印处理器
description: 安装打印处理器
ms.assetid: 4e9e1148-16a3-42f6-a262-1eef014636d0
keywords:
- 打印处理器 WDK，安装
- 安装打印处理器 WDK
- 打印队列 WDK、 打印处理器安装
- 将打印处理器与打印队列 WDK 相关联
- 打印处理器 WDK，将与打印队列相关联
- 打印队列 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bda252290d66e281fa4172cad9ddaa7ffe1d09f0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564669"
---
# <a name="installing-a-print-processor"></a>安装打印处理器





若要安装打印处理器，安装应用程序必须调用后台处理程序的**AddPrintProcessor**函数。 若要将打印处理器与打印队列相关联，列出其 PrintProcessor 条目中的 INF 文件中的文件名称。 此条目必须包含每个打印队列的打印处理器是相关联。 有关详细信息，请参阅[打印机 INF 文件](printer-inf-files.md)。

当安装应用程序调用后台处理程序的**AddPrinter**函数，请使用打印机\_信息\_2 结构作为输入参数，它指定打印处理器的名称 （从 INF 文件中获取）结构成员。 ( **AddPrintProcessor**并**AddPrinter**函数和打印机\_信息\_2 结构 Microsoft Windows SDK 文档中所述。)

### <a name="associating-a-print-processor-with-a-pnp-installed-print-queue"></a>将打印处理器与 PnP 安装打印队列相关联

如果插 (PnP) 管理器检测到并运行 Windows 2000 或 Windows XP 的系统上安装的打印队列和用来安装打印队列的 INF 文件包含 PrintProcessor 条目不是默认 Windows 打印处理器，WinPrint打印处理器不会与打印队列关联。 但是，将安装打印处理器。 （请注意，如果在安装打印队列使用添加打印机向导，打印处理器与打印队列正确关联。 另请注意，在 Microsoft Windows Server 2003 及更高版本的即插即用管理器正确打印处理器将与相关联的打印队列。）

若要将打印处理器与插在 Windows 2000 和 Windows XP 上进行安装的打印队列相关联，包括打印机\_事件\_中的打印机接口 DLL 的初始化情况[ **DrvPrinterEvent** ](https://msdn.microsoft.com/library/windows/hardware/ff548564)函数。 Microsoft Windows Server 2003 和更高版本，不需要添加打印机\_事件\_中的初始化情况**DrvPrinterEvent**函数。

下面的代码示例设置**pPrintProcessor**打印机的成员\_信息\_2 结构的名称将打印处理器，然后调用**SetPrinter**函数 （Windows SDK 文档中所述） 来更新打印机的设置。 请注意，名称中的打印处理器*gszPrintProc* PrintProcessor 项 INF 文件中必须是相同的。

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

### <a href="" id="associating-a-print-processor-with-a-print-queue-during-printer-driver"></a>在打印机驱动程序升级期间将打印处理器与打印队列相关联

当更新的打印机驱动程序时，更新后的打印队列的打印处理器不会更改。 如果新的打印机驱动程序需要特定的打印处理器，打印机接口 DLL [ **DrvUpgradePrinter** ](https://msdn.microsoft.com/library/windows/hardware/ff548648)函数必须设置**pPrintProcessor**的成员打印机\_信息\_2 结构与新的打印处理器的名称。 发生这种情况后，此函数将调用**SetPrinter**更新打印机的设置。 后台处理程序调用**DrvUpgradePrinter**函数一次为每个打印机，这可确保也使用该驱动程序的所有打印机都使用的所需的打印处理器。 下面的代码示例演示了这些点。

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

 

 




