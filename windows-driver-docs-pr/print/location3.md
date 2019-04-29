---
title: Location
description: Location
ms.assetid: cbe6ec7f-36dd-484e-8db6-42e91e69577c
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e403b7dc2056e09d6c63d7063de0fbf0523f999f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63388076"
---
# <a name="location"></a>Location


架构路径：\\Printer.Finishing.Staple.Location

节点类型： 属性

说明： 此属性包含与处装订输出页面的位置相关的所有值项。

位置属性包含两个对子值：**CurrentValue**并**支持**。

### <a name="span-idcurrentvaluespanspan-idcurrentvaluespan-currentvalue"></a><span id="currentvalue"></span><span id="CURRENTVALUE"></span> CurrentValue

架构路径：\\Printer.Finishing.Staple.Location:CurrentValue

节点类型： 值

数据类型： BIDI\_字符串

说明： 当前 staples 收取的 （默认） 位置。

允许使用以下值：

StapleTopLeft

StapleBottomLeft

StapleTopRight

StapleBottomRight

StapleDualLeft

StapleDualRight

StapleDualTop

StapleDualBottom

SaddleStitch

其他

Unknown

### <a name="span-idsupportedspanspan-idsupportedspan-supported"></a><span id="supported"></span><span id="SUPPORTED"></span> 支持

架构路径：\\Printer.Finishing.Staple.Location:Supported

节点类型： 值

数据类型： BIDI\_字符串

说明： 一个以逗号分隔的列表的装订位置支持的所有值。

 

 




