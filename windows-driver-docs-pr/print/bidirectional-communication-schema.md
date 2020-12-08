---
title: 双向通信架构
description: 双向通信架构
keywords:
- 双向通信架构 WDK 打印
- 双向通信架构 WDK 打印
- 属性 WDK 双向通信
- 值 WDK 双向通信
ms.date: 06/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: ef40d270031726cf7e03025776569a426c035daf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797801"
---
# <a name="bidirectional-communication-schema"></a>双向通信架构


双向 (双向) 通信架构是打印机属性的层次结构，其中一些属性是属性，而其他一些是值 (或值项) 。

-   *属性* 是架构层次结构中的节点。 一个属性可以有一个或多个子级，这些子级可以是其他属性或值。 属性可以包含值的列表或其他属性。 它可以表示功能、复合功能或打印系统属性， (如驱动程序名称) 。

-   *值* 是架构层次结构中的叶，表示单个数据项或相关数据项的列表。 值具有名称、数据类型和数据值。 值不能包含子元素。 值可以通过其名称引用，但前提是该名称与作为值父级的属性的架构路径相关联。

例如，以下查询可用于访问 "装订" 属性下的 *已安装* 值。

`\Printer.Finishing.Staple:Installed`

可以通过创建双向扩展文件在中扩展双向架构。 此文件是一个 XML 文件，用于定义特定于特定驱动程序的新架构。 双向扩展文件中的架构是标准打印架构的子集，并使用 XSD 文件 (双向扩展框架) 的构造来定义。

有关架构属性和值的完整列表，请参阅 [双向通信架构层次结构](bidirectional-communication-schema-hierarchy.md)。 若要了解如何构造查询，请参阅 [构造双向通信架构查询](constructing-a-bidi-communication-schema-query.md)。 有关双向通信架构中的属性和值的详细信息，请参阅 [双向通信架构参考](bidi-communications-schema-reference.md)。

安装双向扩展文件的一种简便方法是使文件成为打印机驱动程序的 *依赖文件* 。 有关依赖文件的详细信息，请参阅 [打印机 INF 文件条目](printer-inf-file-entries.md)。
