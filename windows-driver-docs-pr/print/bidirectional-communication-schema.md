---
title: 双向通信架构
description: 双向通信架构
ms.assetid: b15b1aff-623e-4159-ab0f-ce386a1377eb
keywords:
- 双向通信架构 WDK 打印
- 双向通信架构 WDK 打印
- 属性 WDK bidi 通信
- 值 WDK bidi 通信
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2938b1fe9ab1635aa6960cc97662f2821f1f60c8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381110"
---
# <a name="bidirectional-communication-schema"></a>双向通信架构


双向 (bidi) 通信架构是打印机属性，其中一些属性和其他值 （或值项） 的层次结构。

-   一个*属性*是架构层次结构中的节点。 属性可以有一个或多个子级和这些子对象可以是其他属性或值。 属性可以包含一系列值或其他属性。 它可以表示一项功能，复合的功能或打印系统属性 （例如驱动程序名称）。

-   一个*值*是表示单个数据项或一系列相关的数据项目的架构层次结构中的叶节点。 一个值具有名称、 数据类型和数据值。 值不能有子元素。 按其名称，但只有在名称与相关联的值的父属性的架构路径时，可以引用一个值。

例如，可以使用以下查询以访问*已安装*处装订属性下的值。

`\Printer.Finishing.Staple:Installed`

通过创建 bidi 扩展文件，可以在扩展 bidi 架构。 此文件是定义的特定驱动程序特定的新架构的 XML 文件。 Bidi 扩展文件中的架构是标准的打印架构的子集，并且通过使用构造的 XSD 文件 （Bidi 扩展框架） 定义。

架构属性和值的完整列表，请参阅[双向通信架构层次结构](bidirectional-communication-schema-hierarchy.md)。 若要了解如何构造查询，请参阅[构造 Bidi 通信架构查询](constructing-a-bidi-communication-schema-query.md)。 属性和 Bidi 通信架构中的值的详细信息，请参阅[Bidi 通信架构参考](bidi-communications-schema-reference.md)。

安装 bidi 扩展文件的简便方法是使该文件*依赖文件*的打印机驱动程序。 有关依赖文件的详细信息，请参阅[打印机 INF 文件条目](printer-inf-file-entries.md)。
