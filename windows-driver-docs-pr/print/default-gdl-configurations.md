---
title: 默认的 GDL 配置
description: 默认的 GDL 配置
keywords:
- GDL WDK，配置
- 分析器 WDK GDL，创建默认配置
- 配置 WDK GDL，默认配置
- 默认 GDL 配置 WDK
- 配置 WDK GDL，示例
- DefaultOption 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30b09a361c72914abea83c3c8159e84abb56dad9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797317"
---
# <a name="default-gdl-configurations"></a>默认的 GDL 配置


如果客户端没有特定的配置，则可以通过调用 **GetDefaultConfig ( # B1**，请求分析器创建并返回默认配置。 分析器通过为每个参数分配默认值来创建默认配置。 使用 **\* DefaultOption** 指令指定默认值。 **\* DefaultOption** 指令是 **\* 功能** 构造的子条目。 **\* DefaultOption** 应将其值指定为一个构造标记，该标记出现在某个 **\* 选项** 构造中。 有关 **\* DefaultOption**、 **\* 功能** 和 **\* 选项** 的详细信息，请参阅 [用于配置的 GDL 指令](gdl-directives-for-configurations.md)

例如，假设天气参数的默认值为 Sunny。 然后，可以使用以下代码示例来定义默认值。

```cpp
*Feature: Weather
{
   *DefaultOption: Sunny
   *Option: Sunny{}
   *Option: Cloudy{}
}
```

如果缺少 **\* DefaultOption** 指令，则分析器将假定第一个 **\* 选项** 为默认值。

还可以 [更改默认的 GDL 配置](changing-the-default-gdl-configuration.md)。

 

 




