---
title: 安装 Pscript 微型驱动程序
description: 安装 Pscript 微型驱动程序
ms.assetid: 9c48b2b0-c293-4606-bbaa-3fcaca01c300
keywords:
- 微型驱动程序 WDK Pscript 安装
- INF 文件 WDK 打印 Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ccc32feb728606af4095aa4c6908c9249f5508bb
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547959"
---
# <a name="installing-a-pscript-minidriver"></a>安装 Pscript 微型驱动程序





Pscript 微型驱动程序安装要求[打印机 INF 文件](printer-inf-files.md)标识微型驱动程序的文件。 如果打印机型号不受 Microsoft 的打印机 INF 文件，则需要 ntprint.inf，供应商提供的 INF 文件。 INF 文件应引用[打印机 INF 文件的数据部分](printer-inf-file-data-sections.md)并[打印机 INF 文件安装部分](printer-inf-file-install-sections.md)，其定义在 ntprint.inf 中。 对于名为 abc100 微型驱动程序，通常需要使用以下的 INF 文件条目：

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

如果你要提供[插件的用户界面](user-interface-plug-ins.md)或[呈现插件](rendering-plug-ins.md)，您需要包括 INF 文件中的这些组件的名称。 有关安装自定义的代码的信息，请参阅[安装自定义驱动程序组件](installing-customized-driver-components.md)。

 

 




