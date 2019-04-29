---
title: PagesPerSheet
description: PagesPerSheet
ms.assetid: 019c9344-7661-4c39-a441-469d340e61cb
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bb44883862247dfcb156fe13dd6d43bdb54b1b1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353689"
---
# <a name="pagespersheet"></a>PagesPerSheet


架构路径：\\Printer.Layout.NumberUp.PagesPerSheet

节点类型： 属性

说明： 定义可打印的所选介质单面上的逻辑页的数目。 值项的子级的此属性指定每个媒体表的逻辑页的数目和一个数字，每个指定不同数量的每张纸打印的页面列表。

PagesPerSheet 属性包含两个对子值：**CurrentValue**并**支持**。

### <a name="span-idcurrentvaluespanspan-idcurrentvaluespancurrentvalue"></a><span id="currentvalue"></span><span id="CURRENTVALUE"></span>CurrentValue

架构路径：\\Printer.Layout.NumberUp.PagesPerSheet:CurrentValue

节点类型： 值

数据类型： BIDI\_INT

说明： 应放在所选介质单面的逻辑页的数目 （默认值）。

### <a name="span-idsupportedspanspan-idsupportedspansupported"></a><span id="supported"></span><span id="SUPPORTED"></span>支持

架构路径：\\Printer.Layout.NumberUp.PagesPerSheet:Supported

节点类型： 值

数据类型： BIDI\_字符串

说明： 一个以逗号分隔的列表的 PagesPerSheet 支持的所有值。

 

 




