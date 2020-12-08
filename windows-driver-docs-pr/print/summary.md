---
title: 总结
description: 总结
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef90678fdce3b54a815dbce80731ed38e2924006
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806835"
---
# <a name="summary"></a>总结


架构路径： \\ 打印机。状态摘要

节点类型：属性

说明：设备当前状态的简要说明。 这提供了设备状态的高级视图。 只显示最重要的条件。

Summary 属性包含两个子值： **State** 和 **StateReason**。

### <a name="span-idstatespanspan-idstatespanstate"></a><span id="state"></span><span id="STATE"></span>状态

架构路径： \\ 打印机。状态。摘要：状态

节点类型：值

数据类型：双向 \_ 字符串

说明：设备的处理状态。

允许以下值：

闲置

处理

已停止

### <a name="span-idstatereasonspanspan-idstatereasonspanstatereason"></a><span id="statereason"></span><span id="STATEREASON"></span>StateReason

架构路径： \\ Printer. Status。 Summary： StateReason

节点类型：值

数据类型：双向 \_ 字符串

说明：当前打印机状态的最重要原因。 此值可以是由空格分隔的状态原因列表。

允许以下值：

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

 

 




