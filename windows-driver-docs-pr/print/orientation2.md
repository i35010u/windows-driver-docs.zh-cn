---
title: 方向
description: 方向
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c049457bd79b5530fc143c90f610c4eb4f03a55
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807677"
---
# <a name="orientation"></a>方向


架构路径： \\ 打印机的布局。

节点类型：属性

说明：与页面方向相关的属性。 作为此属性的子级的值项是当前页面方向和设备支持的页面方向列表。

"方向" 属性包含两个子值： **CurrentValue** 和 **受支持**。

### <a name="span-idcurrentvaluespanspan-idcurrentvaluespan-currentvalue"></a><span id="currentvalue"></span><span id="CURRENTVALUE"></span> CurrentValue

架构路径： \\ Printer. Layout： CurrentValue

节点类型：值

数据类型：双向 \_ 字符串

说明：当前 (默认) 打印页面的方向。

必须是下列值之一。

纵向

横向

ReversePortrait

ReverseLandscape

### <a name="span-idsupportedspanspan-idsupportedspan-supported"></a><span id="supported"></span><span id="SUPPORTED"></span> 受

架构路径： \\ Printer. Layout：支持

节点类型：值

数据类型：双向 \_ 字符串

说明：以逗号分隔的列表，其中列出了支持的所有值。

 

 




