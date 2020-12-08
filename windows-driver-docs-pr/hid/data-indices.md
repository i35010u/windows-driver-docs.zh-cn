---
title: 数据索引
description: 数据索引
keywords:
- 数据索引 WDK HID
- 为 WDK HID 数据编制索引
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c347fad1f65dd0aee08059ccbcfe500b139902ee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832365"
---
# <a name="data-indices"></a>数据索引





HID 分析器分配一个 *数据索引* ，用于唯一标识顶级集合的 [按钮功能数组](button-capability-arrays.md) 和 [值功能数组](value-capability-arrays.md)中所述的每个使用情况。 从概念上讲，数据索引是从零开始的数组索引，用户模式应用程序或内核模式驱动程序可以使用它来访问报表中的单个控件数据。 分析器将唯一的一组数据索引分配给每个顶级集合支持的每个报表类型。

功能结构通过以下方式交叉引用使用情况和数据索引：

-   描述使用情况的每个功能结构都将设置其 **NotRange** 成员以标识使用情况，并将其 **NotRange DataIndex** 成员设置为使用相应的数据索引。

-   描述使用范围的每个功能结构都设置了其 UsageMin 和 **UsageMax** 成员的 **范围**。 **DataIndexMin** 和 **DataIndexMax** 成员设置为标识使用范围的相应数据索引范围。  (*数据索引范围* 指定连续的数据索引序列;数据索引范围内的数据索引数等于相应使用范围中的使用次数。 ) 

有关如何使用数据索引的详细信息，请参阅 [按数据索引提取和设置控件数据](./interpreting-hid-reports.md)。

 

