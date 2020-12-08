---
title: 事件 \\
description: 事件 \\
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ade10d464871cb5fad7d64ea576e0ef8e25766d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836067"
---
# <a name="event"></a>引发\#\#\#


架构路径： \\ Printer。状态。详细信息\#\#\#

节点类型：属性

说明：基于设备中的事件 Id 生成的事件名称。 每个数字后缀对于给定事件都应是唯一的。 如果设备重复使用特定的数字后缀，则它应留出足够的时间让应用程序确定以前与数字后缀关联的事件是否已过期。 此属性包含描述相关事件的所有值项。

事件 \# \# \# 属性包含两个子值： "名称" 和 "严重性"，是 "[组件](component2.md)" 属性的父项。

### <a name="span-idnamespanspan-idnamespan-name"></a><span id="name"></span><span id="NAME"></span> 名称

架构路径： \\ Printer。状态。详细信息 \# \# \# ：名称

节点类型：值

数据类型：双向 \_ 字符串

说明：当前错误条件的简短说明。 每个组件都有不同的事件名称。

Name 的典型值如下所示：

CoverOpen

纸

DoorOpen

InputTrayMissing

InputTrayMediaSizeChange

InputTrayMediaTypeChange

InputTraySupplyLow

InputTraySupplyEmpty

OutputTrayMissing

OutputTrayAlmostFull

OutputTrayFull

FuserUnderTemperature

FuserOverTemperature

ConsumableLow

ConsumableEmpty

WasteReceptacleAlmostFull

WasteReceptacleFull

### <a name="span-idseverityspanspan-idseverityspan-severity"></a><span id="severity"></span><span id="SEVERITY"></span> 对应

架构路径： \\ Printer. Status。 Summary：详细信息。事件 \# \# \# ：严重性

节点类型：值

数据类型：双向 \_ 字符串

说明：当前事件的严重级别。 打印机确定分配给错误条件的严重性级别。

允许以下值：

信息

警告

严重

 

 




