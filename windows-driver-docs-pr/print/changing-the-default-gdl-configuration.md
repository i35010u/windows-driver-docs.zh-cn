---
title: 更改默认的 GDL 配置
description: 更改默认的 GDL 配置
ms.assetid: ecc4a6ab-869a-402e-b90e-5ad94e0347c3
keywords:
- GDL WDK 配置
- 配置 WDK GDL，默认配置
- 配置 WDK GDL，更改默认配置
- 默认 GDL 配置 WDK
- DefaultOption 指令 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e55c695942305c97d2748d5a39599897697e84d4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347247"
---
# <a name="changing-the-default-gdl-configuration"></a>更改默认的 GDL 配置


**\*DefaultOption**指令本身可能取决于配置。 您可以通过定义内的多个时间的指令来定义不同的默认配置 **\*交换机**并 **\*用例**构造。 但是，必须确保依赖项与不冲突 **\*ConflictPriority**建立在每个参数。

首先应使用默认配置是最安全，因为即使想要显式设置某些参数的值。 完成配置可能包含你不知道的和，将的参数未指定尝试从头开始创建你自己的配置。 此外，GDL 文件可能未定义打算设置一些参数。

例如，假定客户端获取默认配置，并想要更新两个参数为新值。 如果两个参数是今天和天气，客户端查询 date 函数，并查找今天是星期五。 客户端检查来自 Internet 的当前天气并找到天气是 Sunny）。

首先，客户端应验证，通过查看默认快照，今天和天气参数 GDL 文件中定义。 客户端应然后验证 Friday 和 GDL 文件中定义阳光明媚的值。 通过使用 DOM 方法搜索默认快照，它可以验证这些值。 此验证后客户端可以找到持有的默认值用于这些参数在配置中的每个节点，并将其更新为新值。

在其他情况下，配置获取用户输入或检索从持久性存储区。 客户端还可以使用这些配置以获取快照。

 

 




