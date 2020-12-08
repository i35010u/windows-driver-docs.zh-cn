---
title: 隐式 Bin 扩展
description: 隐式 Bin 扩展
keywords:
- 隐式 bin 扩展 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0abd6197b06fe8fb8994d2288c0e05d4a4871689
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835725"
---
# <a name="implicit-bin-extensions"></a>隐式 Bin 扩展


每个 InputBin 或 OutputBin 构造都扩展了包含两个或多个查询的架构。 InputBin 扩展生成四个新的架构值：已安装、级别、媒体媒体和 MediaSize。 OutputBin 扩展会生成两个新的架构值： "已安装" 和 "级别"。

这些架构在 Tcpbidi 文件中的 **InputBins** 和 **OutputBins** 属性下定义。

```cpp
<InputBin name="TopBin" mibName="TRAY 1"/>
```

前面的 InputBin 构造会生成以下四个查询：

```cpp
\Printer.Layout.InputBins.TopBin:Installed
\Printer.Layout.InputBins.TopBin:Level
\Printer.Layout.InputBins.TopBin:MediaType
\Printer.Layout.InputBins.TopBin:MediaSize

<OutputBin name="TopBin" mibName="STANDARD BIN"/>
```

前面的 OutputBin 构造会生成以下两个查询：

```cpp
\Printer.Finishing.OutputBins.TopBin:Installed
\Printer.Finishing.OutputBins.TopBin:Level
```

 

 




