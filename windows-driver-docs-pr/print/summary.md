---
title: 总结
description: 总结
ms.assetid: 8ed412b2-1e7c-440f-8949-a3b1fff09b16
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d583201b00164b6082ed5d5a8f5b173838cb806a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331769"
---
# <a name="summary"></a>总结


架构路径：\\Printer.Status.Summary

节点类型： 属性

说明： 一个简短的设备的当前状态的说明。 这提供了设备状态的高级视图。 显示仅最重要的条件。

摘要属性包含两个对子值：**状态**并**StateReason**。

### <a name="span-idstatespanspan-idstatespanstate"></a><span id="state"></span><span id="STATE"></span>状态

架构路径：\\Printer.Status.Summary:State

节点类型： 值

数据类型： BIDI\_字符串

说明： 该设备的处理状态。

允许使用以下值：

空闲

正在处理

已停止

### <a name="span-idstatereasonspanspan-idstatereasonspanstatereason"></a><span id="statereason"></span><span id="STATEREASON"></span>StateReason

架构路径：\\Printer.Status.Summary:StateReason

节点类型： 值

数据类型： BIDI\_字符串

说明： 当前打印机状态的最重要原因。 此值可以是空格分隔状态原因的列表。

允许使用以下值：

AttentionRequired

DoorOpen

MarkerSupplyEmpty

MarkerSupplyLow

MediaEmpty

MediaJam

MediaLow

MediaNeeded

无

已暂停

OutputAreaAlmostFull

OutputAreaFull

 

 




