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
ms.openlocfilehash: d26e41707d05e822ca0aed3a9cfd7214966a4c73
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206703"
---
# <a name="installing-a-print-processor"></a>安装打印处理器





若要安装打印处理器，安装应用程序必须调用后台处理程序的 **AddPrintProcessor** 函数。 若要将打印处理器与打印队列相关联，请在 PrintProcessor 条目中列出 INF 文件中的文件名。 对于打印处理器要关联到的每个打印队列，都必须包含此项。 有关详细信息，请参阅 [打印机 INF 文件](printer-inf-files.md)。

当安装应用程序调用后台处理程序的 **interactivesession.addprinter** 函数时，使用打印机 \_ 信息 \_ 2 结构作为输入参数，它指定从 INF 文件) 作为结构成员获取的打印处理器 (名称。 Microsoft Windows SDK 文档中介绍了 **AddPrintProcessor** 和 **interactivesession.addprinter** 函数 (和打印机 \_ 信息 \_ 2 结构。 ) 

### <a name="associating-a-print-processor-with-a-pnp-installed-print-queue"></a>将打印处理器与 PnP 安装的打印队列关联

如果即插即用 (PnP) 管理器在运行 Windows 2000 或 Windows XP 的系统上检测并安装打印队列，并且用于安装打印队列的 INF 文件包含除默认的 Windows 打印处理器 WinPrint 之外的 PrintProcessor 项，则打印处理器不会与打印队列关联。 但会安装打印处理器。  (请注意，如果使用 "添加打印机向导" 安装打印队列，打印处理器将与打印队列正确关联。 另请注意，Microsoft Windows Server 2003 和更高版本中的 PnP 管理器会正确地将打印处理器与打印队列关联。 ) 

若要将打印处理器与 Windows 2000 和 Windows XP 上的即插即用安装的打印队列相关联，请 \_ \_ 在打印机接口 DLL 的 [**DrvPrinterEvent**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvprinterevent) 函数中包含打印机事件初始化用例。 对于 Microsoft Windows Server 2003 及更高版本，无需 \_ \_ 在 **DrvPrinterEvent** 函数中添加打印机事件 INITIALIZE case。

下面的代码示例将打印机 INFO 2 结构的 **pPrintProcessor** 成员设置 \_ \_ 为打印处理器的名称，然后调用 Windows SDK 文档) 中描述的 **SetPrinter** (函数来更新打印机的设置。 请注意， *gszPrintProc* 中打印处理器的名称必须与 INF 文件中 PrintProcessor 条目的名称相同。

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

### <a name="associating-a-print-processor-with-a-print-queue-during-printer-driver-upgrade"></a><a href="" id="associating-a-print-processor-with-a-print-queue-during-printer-driver"></a>在打印机驱动程序升级过程中将打印处理器与打印队列关联

更新打印机驱动程序时，不会更改更新的打印队列的打印处理器。 如果新的打印机驱动程序需要特定的打印处理器，则打印机接口 DLL 的 [**DrvUpgradePrinter**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvupgradeprinter) 函数必须将打印机 INFO 2 结构的 **pPrintProcessor** 成员设置 \_ \_ 为新打印处理器的名称。 出现这种情况后，此函数将调用 **SetPrinter** 来更新打印机的设置。 后台处理程序为每台打印机调用一次 **DrvUpgradePrinter** 函数，这可确保使用该驱动程序的所有打印机也使用所需的打印处理器。 下面的代码示例演示了这些要点。

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

 

