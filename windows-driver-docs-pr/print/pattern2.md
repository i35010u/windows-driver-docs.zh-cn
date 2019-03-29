---
title: 模式
description: 模式
ms.assetid: 4c9067dc-03b2-4bee-ad30-df395de357d9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21597e9d7184af64d83e18feae814721cb82e692
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562582"
---
# <a name="pattern"></a>模式


架构路径：\\Printer.Finishing.HolePunch.Pattern

节点类型： 属性

说明： 此属性包含与漏洞可以打孔输出页中的模式相关的所有值项。

Pattern 属性包含两个对子值：**CurrentValue**并**支持**。

### <a name="span-idcurrentvaluespanspan-idcurrentvaluespancurrentvalue"></a><span id="currentvalue"></span><span id="CURRENTVALUE"></span>CurrentValue

架构路径：\\Printer.Finishing.HolePunch.Pattern:CurrentValue

节点类型： 值

数据类型： BIDI\_字符串

说明： 当前的 （默认值） 漏洞打孔模式将应用于输出页面。

允许使用以下值：

TwoHoleUSTop

ThreeHoleUS

TwoHoleDIN

FourHoleDIN

TwentyTwoHoleUS

NineteenHoleUS

TwoHoleMetric

Swedish4Hole

TwoHoleUSSide

FiveHoleUS

SevenHoleUS

Mixed7H4S

Norweg6Hole

Metric26Hole

Metric30Hole

unknown

### <a name="span-idsupportedspanspan-idsupportedspansupported"></a><span id="supported"></span><span id="SUPPORTED"></span>支持

架构路径：\\Printer.Finishing.HolePunch.Pattern:Supported

节点类型： 值

数据类型： BIDI\_字符串

说明： 一个以逗号分隔的列表的打孔模式支持的所有值。

 

 




