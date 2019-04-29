---
title: 驱动程序特定的 Bin
description: 驱动程序特定的 Bin
ms.assetid: 4c014e64-9e82-4058-9ec9-51769102f815
keywords:
- 特定于设备的箱 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ec7f2cbce3af3486ec01fefea5f1820c54510d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360573"
---
# <a name="driver-specific-bins"></a>驱动程序特定的 Bin


你可以随意扩展 bidi 通信架构使用特定于驱动程序的 bin 的名称。 在这种情况下，只有驱动程序将能够识别其他接收器名称。

```cpp
<InputBin name="AAA" mibName="TRAY A"/>
```

前面的代码示例会导致以下四个查询。 前面曾提到一个 InputBin 构造，它会生成四个新查询。

```cpp
\Printer.Layout.InputBins.AAA:Installed
\Printer.Layout.InputBins.AAA:Level
\Printer.Layout.InputBins.AAA:MediaType
\Printer.Layout.InputBins.AAA:MediaSize

<OutputBin name="BBB" mibName="BIN B"/>
```

前面的代码示例会导致以下两个查询。 前面曾提到一个 OutputBin 构造，它会生成两个新查询。

```cpp
\Printer.Finishing.OutputBins.BBB:Installed
\Printer.Finishing.OutputBins.BBB:Level
```

 

 




