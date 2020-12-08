---
title: 组件
description: 组件
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bd81e2540ba1fb23fd763330c3f9ea481faa517
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797619"
---
# <a name="component"></a>组件


架构路径： \\ Printer. Status。 Summary：详细信息。事件 \# \# \# 。组件

数据类型：属性

说明：此属性包含的值项描述了当前事件所影响的打印设备部分。

组件属性包含两个子值：组和名称。

### <a name="span-idgroupspanspan-idgroupspan-group"></a><span id="group"></span><span id="GROUP"></span> 组

架构路径： \\ Printer. Status。 Summary：详细信息。事件 \# \# \# 。组件：组

节点类型：值

数据类型：双向 \_ 字符串

说明：受当前事件影响的组件组。 下一) 中描述的组件组和组件名称 (组合在一起，以确定问题的确切位置。 以下列表包含组的典型值：

InputBin

MediaPath

OutputBins

易耗型产品

### <a name="span-idnamespanspan-idnamespan-name"></a><span id="name"></span><span id="NAME"></span> 名称

架构路径： \\ Printer. Status。 \# \# \#组件：名称

节点类型：值

数据类型：双向 \_ 字符串

说明：受当前事件影响的单个组件的名称。 组合上述) 的组件名称和组件组 (，以确定问题的确切位置。

*Name* 的典型值如下所示：

Tray1

TopBin

LargeCapacityBin

OutputBin1

粉黑色

蓝绿色

 

 




