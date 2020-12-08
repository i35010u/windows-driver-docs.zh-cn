---
title: 驱动程序特定的 Bin
description: 驱动程序特定的 Bin
keywords:
- 设备特定箱 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2fc52601dd8a4dfc1cc15a8daef303a6b47a0635
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797175"
---
# <a name="driver-specific-bins"></a>驱动程序特定的 Bin


可以通过特定于驱动程序的 bin 名称任意扩展双向通信架构。 在这种情况下，只有驱动程序才能识别其他 bin 名称。

```cpp
<InputBin name="AAA" mibName="TRAY A"/>
```

前面的代码示例生成以下四个查询。 回忆一下，InputBin 构造生成四个新查询。

```cpp
\Printer.Layout.InputBins.AAA:Installed
\Printer.Layout.InputBins.AAA:Level
\Printer.Layout.InputBins.AAA:MediaType
\Printer.Layout.InputBins.AAA:MediaSize

<OutputBin name="BBB" mibName="BIN B"/>
```

前面的代码示例生成以下两个查询。 回忆一下，OutputBin 构造会生成两个新的查询。

```cpp
\Printer.Finishing.OutputBins.BBB:Installed
\Printer.Finishing.OutputBins.BBB:Level
```

 

 




