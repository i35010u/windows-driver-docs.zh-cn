---
title: 安装 Pscript 微型驱动程序
description: 安装 Pscript 微型驱动程序
keywords:
- 微型驱动程序 WDK Pscript，安装
- INF 文件 WDK 打印，Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d2a0861520dfeb46555a318fccae14337b441f0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835685"
---
# <a name="installing-a-pscript-minidriver"></a>安装 Pscript 微型驱动程序





安装 Pscript 微型驱动程序需要一个 [打印机 INF 文件](printer-inf-files.md) ，用于标识微型驱动程序的文件。 如果 Microsoft 的打印机 INF 文件（ntprint.inf）不支持打印机型号，则需要供应商提供的 INF 文件。 INF 文件应引用 [打印机 inf 文件数据部分](printer-inf-file-data-sections.md) 和 [打印机 inf 文件安装部分](printer-inf-file-install-sections.md)（在 ntprint.inf 中定义）。 对于名为 abc100 的微型驱动程序，通常需要以下 INF 文件条目：

```cpp
[Manufacturer]
"ABC Printers"
 
[ABC Printers]
"ABC Printer 100 PS" = ABC100.PPD, ABC_Printer_100_PS
 
[ABC100.PPD]
CopyFiles=@ABC100.ppd       ; PPD file.
DataSection=PSCRIPT_DATA    ; PSCRIPT Data Section
DataFile=ABC100.ppd
Include=NTPRINT.INF         ; Include NTPRINT.INF.
Needs=PSCRIPT.OEM           ; Install PSCRIPT.
```

如果你正在提供 [用户界面插件](user-interface-plug-ins.md) 或 [呈现插件](rendering-plug-ins.md)，则需要在 INF 文件中包含这些组件的名称。 有关安装自定义代码的信息，请参阅 [安装自定义驱动程序组件](installing-customized-driver-components.md)。

 

 




