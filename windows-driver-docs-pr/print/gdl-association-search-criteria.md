---
title: GDL 关联搜索条件
description: GDL 关联搜索条件
ms.assetid: f591e944-a6dc-406a-a15e-7af0cc70d7f5
keywords:
- 模板 WDK GDL，将模板与关键字相关联
- WDK GDL，将模板与关键字关联的关键字
- 模板 WDK GDL，关联的搜索条件
- 关联的搜索条件 WDK GDL
- GDL WDK，搜索条目
- GDL WDK 条目
- 无法识别的条目 WDK GDL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f92f230af25594233252c97189733db532c7868c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541330"
---
# <a name="gdl-association-search-criteria"></a>GDL 关联搜索条件


每个数据条目存在根级别或成员的父构造。 如果该条目驻留在根级别中，根级别模板定义的成员列表中搜索限定要与项相关联的第一个模板。 如果构造中找到数据输入，则使用与父构造相关联的模板的成员列表。

搜索成员列表，从最近添加的元素。 搜索成员列表和搜索包含成员列表的模板已被继承模板派生，如果将继续通过名为模板时\*继承条目并继续，直到最旧排序搜索模板的成员列表。

搜索将结束时找到符合条件来表示数据输入的模板。 如果达到列表的末尾时发现不符合要求的模板，将没有模板联系; 保留数据输入调用此类数据条目*无法识别的条目*。 无法识别的数据构造的所有成员也都将无法识别。

 

 




