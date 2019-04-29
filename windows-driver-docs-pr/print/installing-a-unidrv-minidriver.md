---
title: 安装 Unidrv 微型驱动程序
description: 安装 Unidrv 微型驱动程序
ms.assetid: 0efead8f-c413-4ec1-b940-89b57f95345e
keywords:
- Unidrv，微型驱动程序
- 微型驱动程序 WDK Unidrv
- INF 文件 WDK 打印，Unidrv 微型驱动程序
- Unidrv WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9bc374d3c9082802b31ff698b0afa557aac87c4a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366891"
---
# <a name="installing-a-unidrv-minidriver"></a>安装 Unidrv 微型驱动程序





Unidrv 微型驱动程序安装要求[打印机 INF 文件](printer-inf-files.md)标识微型驱动程序的文件。 如果打印机型号不受 Microsoft 的打印机 INF 文件，则需要 ntprint.inf，供应商提供的 INF 文件。 INF 文件应引用[打印机 INF 文件的数据部分](printer-inf-file-data-sections.md)并[打印机 INF 文件安装部分](printer-inf-file-install-sections.md)，其定义在 ntprint.inf 中。 对于名为 abc100 微型驱动程序，通常需要以下 INF 文件条目，如果打印机是双向的支持 TrueType 字体替换，并使用单个资源 DLL:

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

如果你要提供[插件的用户界面](user-interface-plug-ins.md)或[呈现插件](rendering-plug-ins.md)，您需要包括 INF 文件中的这些组件的名称。 有关安装自定义的代码的信息，请参阅[安装自定义驱动程序组件](installing-customized-driver-components.md)。

 

 




