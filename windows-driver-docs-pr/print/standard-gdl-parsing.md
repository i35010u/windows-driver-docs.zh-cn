---
title: 标准 GDL 分析
description: 标准 GDL 分析
ms.assetid: 089bba58-e29f-428a-ab54-4413edca1d0c
keywords:
- GDL WDK 分析器
- 分析器 WDK GDL，标准分析
- 分析 GDL 数据 WDK
- 标准 GDL 分析 WDK
- 默认 GDL 分析 WDK
- 标准分析器筛选器 WDK GDL
- SPF WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2544d7729d678297224c6adb0f8b3925fa577a1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389474"
---
# <a name="standard-gdl-parsing"></a>标准 GDL 分析


默认值或标准分析器筛选器 (SPF) 作为其输入原始快照树 （即，XML 快照，该分析器会生成，属性节点在其中包含与 CDATA 元素仅原始的未分析的值），并执行其他语义验证和处理。

在这种处理，SPF 将 CDATA 的原始值解释为指定的绑定到属性节点和正确表示为一个或多个标准的 XML 数据类型的值的属性节点中添加新的 XML 元素的模板的数据类型。 结果是经过修饰的 XML 快照树，使客户端可以访问作为 XML 数据类型元素的值。

该处理还包括的成员，检查是否存在特性、 默认值初始化属性和生成的 XML 表示形式的结果树中包含的附加属性值的分析，multiply 处理定义元素。 如果需要还会生成警告和错误消息。 由特定的模板指令定向执行的处理。

 

 




