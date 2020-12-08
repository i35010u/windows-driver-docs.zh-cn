---
title: Finishing
description: Finishing
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: af721f282f578935f8d2bdd27a206e89b6a37ab4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797075"
---
# <a name="finishing"></a>Finishing


架构路径： \\ Printer .. 装帧

节点类型：属性

装帧属性包含有关在打印完成后执行的操作的数据。 这包括文档是否可以逐份打印、装订、打孔以及有关可用输出容器的信息。

装帧属性包含两个子值： CollationSupported 和 JogOffsetSupported;它还是 " [装订](staple3.md)"、" [HolePunch](holepunch3.md)" 和 " [OutputBins](outputbins2.md) " 属性的父项。

### <a name="span-idcollationsupportedspanspan-idcollationsupportedspan-collationsupported"></a><span id="collationsupported"></span><span id="COLLATIONSUPPORTED"></span> CollationSupported

架构路径： \\ Printer .. 装帧： CollationSupported

节点类型：值

数据类型：双向 \_ BOOL

说明：指示打印机是否支持打印文档的硬件排序规则。 如果 **为 TRUE**，则支持排序规则;如果 **为 FALSE**，则不支持排序规则。

### <a name="span-idjogoffsetsupportedspanspan-idjogoffsetsupportedspan-jogoffsetsupported"></a><span id="jogoffsetsupported"></span><span id="JOGOFFSETSUPPORTED"></span> JogOffsetSupported

架构路径： \\ Printer .. 装帧： JogOffsetSupported

节点类型：值

数据类型：双向 \_ BOOL

描述：确定打印机是否支持将打印作业的单独副本放入交错组的输出送纸器中的单独打印作业。 如果 **为 TRUE**，则打印机支持角拐偏移量;如果 **为 FALSE**，则打印机不支持此功能。

 

 




