---
title: GDL 关联搜索条件
description: GDL 关联搜索条件
keywords:
- 模板 WDK GDL，将模板与关键字关联
- 关键字 WDK GDL，将模板与关键字关联
- 模板 WDK GDL，关联搜索条件
- 关联搜索条件 WDK GDL
- GDL WDK，搜索条目
- GDL WDK，项
- 无法识别的条目 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d5c0c0133453744d1945596935d3de7332d6876
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797039"
---
# <a name="gdl-association-search-criteria"></a>GDL 关联搜索条件


每个数据条目都存在于根级别或作为父构造的成员。 如果该项位于根级别，则会在根级别模板定义的成员列表中搜索符合该条目的第一个模板。 如果在构造中找到数据输入，则使用与父构造关联的模板的成员列表。

搜索成员列表，并以最近添加的元素开头。 如果已搜索 "成员" 列表，并且包含 "成员" 列表的模板已从继承的模板派生，则搜索将使用继承项命名的模板继续， \* 直到搜索了最早的模板的成员列表。

如果找到了限定为表示数据输入的模板，搜索将结束。 如果在到达列表的末尾时找不到符合条件的模板，则不使用模板关联的数据输入将保留;此类数据条目称为 "未 *标识的条目*"。 无法识别的数据构造的所有成员也将无法识别。

 

 




