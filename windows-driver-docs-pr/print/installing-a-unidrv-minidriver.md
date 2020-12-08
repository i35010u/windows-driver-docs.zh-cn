---
title: 安装 Unidrv 微型驱动程序
description: 安装 Unidrv 微型驱动程序
keywords:
- Unidrv、微型驱动程序
- 微型驱动程序 WDK Unidrv
- INF 文件 WDK 打印，Unidrv 微型驱动程序
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a95f1bd876b1c9947ac8ea93e0b1b493153ebfe2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796719"
---
# <a name="installing-a-unidrv-minidriver"></a>安装 Unidrv 微型驱动程序





安装 Unidrv 微型驱动程序需要一个 [打印机 INF 文件](printer-inf-files.md) ，用于标识微型驱动程序的文件。 如果 Microsoft 的打印机 INF 文件（ntprint.inf）不支持打印机型号，则需要供应商提供的 INF 文件。 INF 文件应引用 [打印机 inf 文件数据部分](printer-inf-file-data-sections.md) 和 [打印机 inf 文件安装部分](printer-inf-file-install-sections.md)（在 ntprint.inf 中定义）。 对于名为 abc100 的微型驱动程序，通常需要以下 INF 文件项，如果打印机是双向的，则支持 TrueType 字体替换，并使用单个资源 DLL：

```cpp
[Manufacturer]
"ABC Printers"
 
[ABC Printers]
"ABC Printer 100" = ABC100.GPD, ABC_Printer_100
 
[ABC100.GPD]
CopyFiles=@ABCres.dll,@ABC100.gpd  ;Resource DLL and GPD file
DataSection=UNIDRV_BIDI_DATA       ;Unidrv Data Section
DataFile=ABC100.gpd
Include=NTPRINT.INF                ;Include NTPRINT.INF.
Needs=TTFSUB.OEM,UNIDRV_BIDI.OEM   ;Install TrueType subs, Unidrv,
  ;    and PJL language monitor.
```

如果你正在提供 [用户界面插件](user-interface-plug-ins.md) 或 [呈现插件](rendering-plug-ins.md)，则需要在 INF 文件中包含这些组件的名称。 有关安装自定义代码的信息，请参阅 [安装自定义驱动程序组件](installing-customized-driver-components.md)。

 

 




