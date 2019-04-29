---
title: GDL 模板继承
description: GDL 模板继承
ms.assetid: 0e3271ee-6b58-4f57-a0be-18715705604f
keywords:
- GDL WDK 模板
- 模板 WDK GDL，继承
- 继承 WDK GDL
- WDK GDL，基于继承的架构的架构
- 模板 WDK GDL，派生模板
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 841457bcc6091b6b4d2a1e1ce520db1466674740
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390614"
---
# <a name="gdl-template-inheritance"></a>GDL 模板继承


由定义两个 GDL 模板之间的关系*继承*。 模板可以从只能有一个其他模板继承属性。 许多模板可以继承一个基本模板。 不支持多重继承 （即，从多个模板继承）。

模板继承创建 compact 定义、 满足简单而清楚的方法，表示一种基本类型的变体的需要和清楚地显示的结构和组织的数据。 模板继承还可以将扩展并在基础框架上构建而无需更改或重新定义的基础框架。

因为数据的内容取决于构造的上下文，不会通过一个 XML 类型的架构定义模板关系。 例如，\*选项构造，它将显示在 PaperSize\*功能具有不同的成员，比\*将显示在解析的选项构造\*功能。 通过使用面向对象的概念，可以是继承的无歧义地精确数据构造之间的关系。

模板继承还要求您了解数据的结构。 例如，所有\*功能构造共享共有一些属性。 基本功能模板最适当地定义这些属性。 然后可以通过添加特定于功能的属性或限制派生的基模板中的特定功能定义。 从基本功能模板派生的每个模板可确保所有派生的模板继承的所有基本通用的所有功能定义的属性。 如果您始终要考虑哪些属性应定义特定的模板和哪些属性应保持为派生模板，您可以集中精力组织、 结构和数据之间的关系。

 

 




