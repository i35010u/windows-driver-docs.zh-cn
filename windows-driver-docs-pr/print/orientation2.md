---
title: Orientation
description: Orientation
ms.assetid: a3bd9d67-200f-4739-ad0e-ff7fd2eb20a3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c288d783764876a8c0f1e1fb72af312f9eec7fd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362749"
---
# <a name="orientation"></a>Orientation


架构路径：\\Printer.Layout.Orientation

节点类型： 属性

说明： 与页面方向关联的属性。 值项的子级的此属性是当前的页面方向和一系列设备支持的页面方向。

方向属性包含两个对子值：**CurrentValue**并**支持**。

### <a name="span-idcurrentvaluespanspan-idcurrentvaluespan-currentvalue"></a><span id="currentvalue"></span><span id="CURRENTVALUE"></span> CurrentValue

架构路径：\\Printer.Layout.Orientation:CurrentValue

节点类型： 值

数据类型： BIDI\_字符串

说明： 将在其中打印页的当前 （默认值） 方向。

必须是以下值之一。

Portrait

Landscape

ReversePortrait

ReverseLandscape

### <a name="span-idsupportedspanspan-idsupportedspan-supported"></a><span id="supported"></span><span id="SUPPORTED"></span> 支持

架构路径：\\Printer.Layout.Orientation:Supported

节点类型： 值

数据类型： BIDI\_字符串

说明： 一个以逗号分隔列表的所有方向的支持的值。

 

 




