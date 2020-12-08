---
title: 标准 GDL 分析
description: 标准 GDL 分析
keywords:
- GDL WDK，分析器
- 分析器 WDK GDL，标准分析
- 分析 GDL 数据 WDK
- 标准 GDL 分析 WDK
- 默认 GDL 分析 WDK
- 标准分析器-筛选 WDK GDL
- SPF WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a0e32d3899e2c0b146ff4210622c74a46912d6f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806879"
---
# <a name="standard-gdl-parsing"></a>标准 GDL 分析


默认的或标准的分析器筛选器 (SPF) 会将原始快照树作为其输入，该 (树为：分析器生成的 XML 快照，其中，属性节点仅将原始未分析值作为 CDATA 元素包含) 并执行其他语义验证和处理。

在此处理过程中，SPF 将原始值 CDATA 解释为绑定到 attribute 节点的模板所指定的数据类型，并在 "属性" 节点中添加新的 XML 元素，这些元素可将值正确表示为一个或多个标准 XML 数据类型。 结果是一个修饰的 XML 快照树，它使客户端能够访问作为 XML 数据类型元素的值。

处理还包括对成员的存在检查、属性值的分析、对定义的属性的多次处理、默认的初始化属性以及包含其他元素的结果树的 XML 表示形式的生成。 如果需要，也会生成警告消息和错误消息。 执行的处理由特定模板指令定向。

 

 




