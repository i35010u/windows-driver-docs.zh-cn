---
title: 更改默认的 GDL 配置
description: 更改默认的 GDL 配置
keywords:
- GDL WDK，配置
- 配置 WDK GDL，默认配置
- 配置 WDK GDL，更改默认配置
- 默认 GDL 配置 WDK
- DefaultOption 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e40491de506376b06f81fb88b650e9cd49e9ff59
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797727"
---
# <a name="changing-the-default-gdl-configuration"></a>更改默认的 GDL 配置


**\* DefaultOption** 指令本身可能取决于配置。 您可以定义不同的默认配置，方法是在 **\* Switch** 和 **\* Case** 构造中多次定义指令。 但是，必须确保依赖项不会与为每个参数建立的 **\* ConflictPriority** 冲突。

你应从默认配置开始，因为它是最安全的，即使你打算显式设置参数的某些值。 完整的配置可能包含您无法识别的参数，如果您尝试从头开始创建自己的配置，则不会指定这些参数。 此外，GDL 文件可能不会定义你计划设置的一些参数。

例如，假设客户端获取默认配置，并且想要将两个参数更新为新值。 如果这两个参数为 "今天" 和 "天气"，则客户端将查询 date 函数并发现今天是星期五。 客户端从 Internet 检查当前天气，并发现天气是 Sunny) 。

首先，客户端应通过查看默认快照来验证 "今天" 和 "天气" 参数是否已在 GDL 文件中定义。 然后，客户端应验证 GDL 文件中是否定义了星期五和 Sunny 值。 它可以通过使用 DOM 方法搜索默认快照来验证这些值。 在此验证之后，客户端可以找到为配置中的每个参数保留默认值的节点，然后将其更新为新值。

在其他情况下，将从用户输入获取配置，或者从永久性存储中检索配置。 客户端还可以使用这些配置来获取快照。

 

 




