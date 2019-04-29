---
title: 默认的 GDL 配置
description: 默认的 GDL 配置
ms.assetid: 9963513b-52dc-4fb7-8f85-abca2975c36d
keywords:
- GDL WDK 配置
- 分析器 WDK GDL，创建默认配置
- 配置 WDK GDL，默认配置
- 默认 GDL 配置 WDK
- 配置 WDK GDL，示例
- DefaultOption 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88d88d518b890860cce0f1e05d614425fd19d636
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384954"
---
# <a name="default-gdl-configurations"></a>默认的 GDL 配置


如果客户端不具有任何特定的配置，它可以请求创建并返回通过调用默认配置的分析器**GetDefaultConfig()**。 分析器通过将默认值分配给每个参数创建的默认配置。 通过使用指定的默认值 **\*DefaultOption**指令。  **\*DefaultOption**指令为的子入口**\*功能**构造。 **\*DefaultOption**应指定为其值将出现在其中一个构造标记之一**\*选项**构造。 有关详细信息 **\*DefaultOption**， **\*功能**，以及**\*选项**，请参阅[GDL指令的配置](gdl-directives-for-configurations.md)

例如，假定天气参数的默认值是 Sunny。 然后，可以使用下面的代码示例来定义默认值。

```cpp
*Feature: Weather
{
   *DefaultOption: Sunny
   *Option: Sunny{}
   *Option: Cloudy{}
}
```

如果 **\*DefaultOption**指令缺失，分析器将假定的第一个**\*选项**是默认值。

此外可以[更改默认 GDL 配置](changing-the-default-gdl-configuration.md)。

 

 




