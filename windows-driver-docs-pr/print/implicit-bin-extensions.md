---
title: 隐式 Bin 扩展
description: 隐式 Bin 扩展
ms.assetid: 2aaa9e48-59f9-4c87-b592-ed60469cf747
keywords:
- 隐式 bin 扩展 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bed3da789f12da3f0fb45c38316cc648b5ad800e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63340912"
---
# <a name="implicit-bin-extensions"></a>隐式 Bin 扩展


每个 InputBin 或 OutputBin 构造与两个或多个查询来扩展架构。 InputBin 扩展生成四个新的架构值：已安装，级别、 媒体类型，以及 MediaSize。 OutputBin 扩展插件将生成两个新的架构值：已安装和级别。

下 Tcpbidi.xsd 文件中定义这些架构**InputBins**并**OutputBins**属性。

```cpp
<InputBin name="TopBin" mibName="TRAY 1"/>
```

上述 InputBin 构造中的以下四个查询的结果：

```cpp
\Printer.Layout.InputBins.TopBin:Installed
\Printer.Layout.InputBins.TopBin:Level
\Printer.Layout.InputBins.TopBin:MediaType
\Printer.Layout.InputBins.TopBin:MediaSize

<OutputBin name="TopBin" mibName="STANDARD BIN"/>
```

上述 OutputBin 构造中的以下两个查询的结果：

```cpp
\Printer.Finishing.OutputBins.TopBin:Installed
\Printer.Finishing.OutputBins.TopBin:Level
```

 

 




