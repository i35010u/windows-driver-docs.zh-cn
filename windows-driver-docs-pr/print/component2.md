---
title: 组件
description: 组件
ms.assetid: 15cc741e-5919-4d71-802b-519494827722
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4481b65a74fa282f69a39f3b4bec63945111490b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353259"
---
# <a name="component"></a>组件


架构路径：\\Printer.Status.Summary:Detailed。事件\#\#\#。组件

数据类型： 属性

说明： 此属性包含说明的一部分打印设备受影响的当前事件的值项。

组件属性包含两个对子值：组和名称。

### <a name="span-idgroupspanspan-idgroupspan-group"></a><span id="group"></span><span id="GROUP"></span> 组

架构路径：\\Printer.Status.Summary:Detailed。事件\#\#\#。组件组：

节点类型： 值

数据类型： BIDI\_字符串

说明： 受影响的当前事件的组件组。 组合的组件组和组件名称 （介绍下一步） 以确定问题的确切位置。 以下列表包含组的典型值：

InputBin

MediaPath

OutputBins

易耗型产品

### <a name="span-idnamespanspan-idnamespan-name"></a><span id="name"></span><span id="NAME"></span> 名称

架构路径：\\Printer.Status.Detailed.Event\#\#\#。组件名称：

节点类型： 值

数据类型： BIDI\_字符串

说明： 受影响的当前事件的各个组件的名称。 组件名称和 （如上所示） 的组件组组合以确定问题的确切位置。

典型值为*名称*如下所示：

Tray1

TopBin

LargeCapacityBin

OutputBin1

Toner.Black

Ink.Cyan

 

 




