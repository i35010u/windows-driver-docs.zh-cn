---
title: 路径名
description: 路径名
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9452da06e20fbd4cfa3ec58b3f7e45ee0157b5ec
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794269"
---
# <a name="name"></a>\[名称\]


架构路径： \\ Printer。 \[路径名\]

节点类型：属性

说明：此属性是供应商映射的可执行名称。 该名称对应于此可执行的供应商特定的唯一 ID。 此 ID 允许具有相同类型和颜色组合的多个耗材。 \[Name \] 属性始终是必需的，并且名称不能包含任何空格。

此属性包含以下子值：

类型

颜色

已安装

Level

模式

### <a name="span-idtypespanspan-idtypespan-type"></a><span id="type"></span><span id="TYPE"></span> 类别

架构路径： \\ Printer。 \[名称 \] 。类别

节点类型：值

说明：此值表示所引用的可执行类型。

以下预定义类型可用：

墨迹

盒

开发人员

FuserOil

Wax

WasteToner

WasteInk

WasteWax

供应商可以添加特定于其打印过程或打印设备的值。

### <a name="span-idcolorspanspan-idcolorspan-color"></a><span id="color"></span><span id="COLOR"></span> 颜色

架构路径： \\ Printer。 \[名称 \] 。颜色

节点类型：双向 \_ 字符串

说明：此值表示所引用的可执行对象的颜色。 此数据值是可选的，因为某些类型的可执行文件实际上并没有与之关联的颜色。

预定义了以下颜色类型。

黑色

蓝色

颜色

蓝

灰色

绿色

洋红色

PhotoBlack

PhotoColor

PhotoCyan

PhotoMagenta

PhotoYellow

Red

白色

Yellow

每个供应商可以添加特定于其打印过程和设备的任何值。

### <a name="span-idinstalledspanspan-idinstalledspan-installed"></a><span id="installed"></span><span id="INSTALLED"></span> 随

架构路径： \\ Printer。 \[名称 \] 。随

节点类型：值

数据类型：双向 \_ BOOL

说明：该值指示是否在设备上安装了类型和颜色描述的可耗用项。

### <a name="span-idlevelspanspan-idlevelspan-level"></a><span id="level"></span><span id="LEVEL"></span> 调配

架构路径： \\ Printer。 \[名称 \] 。调配

节点类型：值

数据类型：双向 \_ INT

说明：此值表示所引用的可执行的当前级别。 此值的单位为百分比点。 完全级别的值将为100，空级别的值将为0。 如果无法度量级别，则应返回值-1 (未知) 。

### <a name="span-idmodelspanspan-idmodelspan-model"></a><span id="model"></span><span id="MODEL"></span> Model

架构路径： \\ Printer。 \[名称 \] 。模式

节点类型：值

数据类型：双向 \_ 字符串

说明：一个可选值，表示所引用的可执行对象的供应商模型指示器。 通过此值，客户端可以精确区分设备中安装的特定类型和颜色组合的版本。

 

 




