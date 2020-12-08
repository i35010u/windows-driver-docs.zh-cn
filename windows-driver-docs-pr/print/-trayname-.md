---
title: '\ TrayName \ (InputBins) '
description: '\ TrayName \ (InputBins) '
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7693a8fe87151611662012f23e236d7f95721d17
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794267"
---
# <a name="trayname-inputbins"></a>\[TrayName \] (InputBins) 


架构路径： \\ InputBins。 \[TrayName\]

节点类型：属性

说明：输入送纸器的 IHV 映射属性名称。 IHV 可以使用以下列表中的名称为输入纸盒映射特定于 IHV 的托盘名称。

Tray1

Tray2

Trayxx (xx 为任意正整数) 

TopBin

MiddleBin

BottomBin

LargeCapacityBin

ManualBin

EnvelopeBin

EnvelopeManual

MultiPurposeBin

\[TrayName \] 属性包含以下子值：

已安装

MediaSize

MediaColor

容量

Level

### <a name="span-idinstalledspanspan-idinstalledspan-installed"></a><span id="installed"></span><span id="INSTALLED"></span> 随

架构路径： \\ InputBins。 \[TrayName \] ：已安装

节点类型：值

数据类型：双向 \_ BOOL

说明：指示 \[ 设备上是否已安装 TrayName 引用的 bin \] 。 如果 **为 TRUE**，则将在设备上安装 bin;如果 **为 FALSE**，则不会在设备上安装 bin。

### <a name="span-idmediasizespanspan-idmediasizespan-mediasize"></a><span id="mediasize"></span><span id="MEDIASIZE"></span> MediaSize

架构路径： \\ InputBins。 \[TrayName \] ： MediaSize

节点类型：值

数据类型：双向 \_ 字符串

说明：当前所引用的输入纸盒中可用媒体的大小。 这些值应符合 IEEE-ISTO PWG Standard 5101.1。
允许使用以下值： na \_ 法律 \_ 8.5 x14in

na \_ 字母 \_ 8.5 x11in

iso \_ a4 \_ 210x297mm

iso \_ c5 \_ 162x229mm

iso \_ dl \_ 110x220mm

jis \_ b4 \_ 257x364mm

### <a name="span-idmediatypespanspan-idmediatypespan-mediatype"></a><span id="mediatype"></span><span id="MEDIATYPE"></span> MediaType

架构路径： \\ InputBins。 \[TrayName \] ：媒体媒体

节点类型：值

数据类型：双向 \_ 字符串

说明：当前引用的输入纸盒中可用的媒体类型。 这些值应符合 IEEE-ISTO PWG Standard 5101.1。
允许使用以下值： cardstock

信封 (envelope)

标签

图像

设计

信纸-喷墨

Transparency — 透明度

其他

### <a name="span-idmediacolorspanspan-idmediacolorspan-mediacolor"></a><span id="mediacolor"></span><span id="MEDIACOLOR"></span> MediaColor

架构路径： \\ InputBins。 \[TrayName \] ： MediaColor

节点类型：值

数据类型：双向 \_ 字符串

说明：当前引用的输入纸盒中可用媒体的颜色。 这些值应符合 IEEE-ISTO PWG Standard 5101.1。
允许使用以下值：白色

pink

yellow

爱好者

金麒麟色

blue

green

红色

灰色

乳白色

orange

无颜色

未知

### <a name="span-idfeeddirectionspanspan-idfeeddirectionspan-feeddirection"></a><span id="feeddirection"></span><span id="FEEDDIRECTION"></span> FeedDirection

架构路径： \\ InputBins。 \[TrayName \] ： FeedDirection

节点类型：值

数据类型：双向 \_ 字符串

说明：指示纸张的哪个边缘首先在当前引用的输入纸盒中输入媒体路径，并且必须是下列值之一：

LongEdgeFirst

ShortEdgeFirst

### <a name="span-idcapacityspanspan-idcapacityspan-capacity"></a><span id="capacity"></span><span id="CAPACITY"></span> 功能

架构路径： \\ InputBins。 \[TrayName \] ：容量

节点类型：值

数据类型：双向 \_ INT

说明：当前引用的输入纸盒的容量（以工作表为表）。

### <a name="span-idlevelspanspan-idlevelspan-level"></a><span id="level"></span><span id="LEVEL"></span> 调配

架构路径： \\ InputBins。 \[TrayName \] ：级别

节点类型：值

数据类型：双向 \_ INT

说明：当前引用的输入纸盒中剩余的容量量，以百分比表示。 完全纸盒的值为100，而空纸盒的值为0。 如果级别不可度量，则值为-1 (指示应返回未知级别) 。

 

 




