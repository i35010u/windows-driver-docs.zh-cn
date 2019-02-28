---
title: '\ 名称'
description: '\ 名称'
ms.assetid: 5259ea1a-a251-479b-88f1-711d5933868a
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60ad341ded00ca35003f72d070765794133ffe1b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544005"
---
# <a name="name"></a>\[名称\]


架构路径：\\Printer.Consumables。\[名称\]

节点类型： 属性

说明： 此属性是供应商映射可使用名称。 名称对应于此可使用的特定于供应商的唯一 ID。 此 ID 可以与相同的类型和颜色组合多个消费品的可能性。 \[名称\]并总是必需的属性和名称不能包含任何空格。

此属性包含以下子值：

在任务栏的搜索框中键入

颜色

已安装

级别

模式

### <a name="span-idtypespanspan-idtypespan-type"></a><span id="type"></span><span id="TYPE"></span> Type

架构路径：\\Printer.Consumables。\[名称\]。类型

节点类型： 值

说明： 此值表示的类型的引用可使用。

提供了以下预定义的类型：

墨迹

墨粉

开发人员

FuserOil

蜡

WasteToner

WasteInk

WasteWax

供应商可以添加特定于其打印进程或打印设备的值。

### <a name="span-idcolorspanspan-idcolorspan-color"></a><span id="color"></span><span id="COLOR"></span> Color

架构路径：\\Printer.Consumables。\[名称\]。颜色

节点类型： BIDI\_字符串

说明： 此值表示引用可使用的颜色。 此数据值是可选的因为某些类型的可使用实际上不具有与其关联的颜色。

预定义以下颜色类型。

黑色

蓝色

颜色

蓝绿色

灰色

厚︹

洋红色

PhotoBlack

PhotoColor

PhotoCyan

PhotoMagenta

PhotoYellow

红色

白色

独︹

每个供应商可以将任何特定的值添加到其打印进程和设备。

### <a name="span-idinstalledspanspan-idinstalledspan-installed"></a><span id="installed"></span><span id="INSTALLED"></span> 安装

架构路径：\\Printer.Consumables。\[名称\]。安装

节点类型： 值

数据类型： BIDI\_BOOL

说明： 此值指示是否在设备上安装的可使用项的类型和颜色描述。

### <a name="span-idlevelspanspan-idlevelspan-level"></a><span id="level"></span><span id="LEVEL"></span> 级别

架构路径：\\Printer.Consumables。\[名称\]。级别

节点类型： 值

数据类型： BIDI\_INT

说明：此值表示引用可使用的当前级别。 此值的单位是百分比。 完全级别将具有的值为 100，并且空级别值为 0。 如果级别不是可衡量的则返回值-1 （未知）。

### <a name="span-idmodelspanspan-idmodelspan-model"></a><span id="model"></span><span id="MODEL"></span> 模型

架构路径：\\Printer.Consumables。\[名称\]。模型

节点类型： 值

数据类型：BIDI\_字符串

说明： 一个可选值，表示被引用可使用供应商模型指示符。 此值允许客户端将完全可使用安装在设备的特定类型和颜色组合的哪个版本区分开来。

 

 




