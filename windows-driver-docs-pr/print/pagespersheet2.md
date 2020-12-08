---
title: PagesPerSheet
description: PagesPerSheet
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: aa902515a383c1150da096fbdd2125f821b196c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807649"
---
# <a name="pagespersheet"></a>PagesPerSheet


架构路径： \\ NumberUp. PagesPerSheet

节点类型：属性

描述：定义可在选定媒体的一侧上打印的逻辑页数。 作为此属性的子级的值项指定了每个媒体表的当前逻辑页数和一个数字列表，每个页面指定了不同的页数。

PagesPerSheet 属性包含两个子值： **CurrentValue** 和 **支持**。

### <a name="span-idcurrentvaluespanspan-idcurrentvaluespancurrentvalue"></a><span id="currentvalue"></span><span id="CURRENTVALUE"></span>CurrentValue

架构路径： \\ NumberUp. PagesPerSheet： CurrentValue

节点类型：值

数据类型：双向 \_ INT

说明：当前 (默认值) 应置于所选媒体一侧的逻辑页的数目。

### <a name="span-idsupportedspanspan-idsupportedspansupported"></a><span id="supported"></span><span id="SUPPORTED"></span>受支持

架构路径： \\ NumberUp. PagesPerSheet：受支持

节点类型：值

数据类型：双向 \_ 字符串

说明： PagesPerSheet 支持的所有值的逗号分隔列表。

 

 




