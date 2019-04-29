---
title: 数据索引
description: 数据索引
ms.assetid: 84577544-515a-4fdc-86e5-518182c6c461
keywords:
- 数据编制索引 WDK HID
- 索引 WDK HID 数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d1fdb684c05c16f07998c25814f401bdd09d8ad
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390335"
---
# <a name="data-indices"></a>数据索引





HID 分析器将分配*数据索引*，用于唯一标识每个使用情况的顶级集合中所述[按钮功能数组](button-capability-arrays.md)和[值功能数组](value-capability-arrays.md). 从概念上讲，数据索引是用户模式应用程序或内核模式驱动程序可用于访问报表中的单个控件数据的从零开始的数组索引。 分析器将一组唯一的数据索引分配给每个顶级集合支持每种报告类型。

功能结构交叉引用用法和数据的索引，如下所示：

-   介绍了使用情况的每个功能结构具有其**NotRange.Usage**成员集来确定使用情况并将其**NotRange.DataIndex**成员集的使用情况信息的相应数据索引。

-   每个描述使用范围的功能结构具有其**Range.UsageMin**并**Range.UsageMax**成员集能够识别的使用情况范围并将其**Range.DataIndexMin**并**Range.DataIndexMax**成员集标识的使用范围的相应数据索引范围。 (*数据编制索引范围*指定的数据索引; 一个连续的序列和数据索引范围中的数据索引的数目是否等于在相应的使用情况范围内的数。)

有关如何使用数据索引的详细信息，请参阅[提取和设置控制数据的数据索引](extracting-and-setting-control-data-by-data-indices.md)。

 

 




