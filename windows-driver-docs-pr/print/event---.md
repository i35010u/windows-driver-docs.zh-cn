---
title: Event\ \ \
description: Event\ \ \
ms.assetid: a3b0b3f1-03d6-4309-9efe-d2588c7240cb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a8a68c1b668ad98fe333b55db5bb21726f67dc33
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519319"
---
# <a name="event"></a>事件\#\#\#


架构路径：\\Printer.Status.Detailed.Event\#\#\#

节点类型： 属性

说明： 一个生成基于事件 Id 的设备中的事件名称。 每个数字后缀应是唯一的给定的事件。 如果设备重复使用特定的数字后缀，则应允许应用程序以确定是否已过期之前的数字后缀与关联的事件足够的时间。 此属性包含的所有值条目描述所讨论的事件。

事件\#\# \#属性中含有两个对子值名称和严重性，并且是父[组件](component2.md)属性。

### <a name="span-idnamespanspan-idnamespan-name"></a><span id="name"></span><span id="NAME"></span> 名称

架构路径：\\Printer.Status.Detailed.Event\#\#\#： 名称

节点类型： 值

数据类型： BIDI\_字符串

当前的错误条件的说明： 一个简短的说明。 有不同的事件的每个组件的名称。

名称的典型值如下所示：

CoverOpen

卡纸问题

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

### <a name="span-idseverityspanspan-idseverityspan-severity"></a><span id="severity"></span><span id="SEVERITY"></span> 严重级别

架构路径：\\Printer.Status.Summary:Detailed。事件\#\#\#： 严重性

节点类型： 值

数据类型： BIDI\_字符串

说明： 当前事件的严重性级别。 打印机确定分配到的错误条件的严重性级别。

允许使用以下值：

信息性

警告

严重

 

 




