---
title: '\ TrayName\ (InputBins)'
description: '\ TrayName\ (InputBins)'
ms.assetid: 7fa03413-5b95-443f-9b0f-75d82d0e41cf
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e670d7a572555493412f1a6cf86775170750871
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372857"
---
# <a name="trayname-inputbins"></a>\[TrayName\] (InputBins)


架构路径：\\Printer.Layout.InputBins。\[TrayName\]

节点类型： 属性

说明： 送纸器 IHV 映射属性名称。 IHV 可以 IHV 特定送纸器将名称映射为送纸器使用与下面的列表的名称。

Tray1

Tray2

Trayxx (xx 任意正整数)

TopBin

MiddleBin

BottomBin

LargeCapacityBin

ManualBin

EnvelopeBin

EnvelopeManual

MultiPurposeBin

\[TrayName\]属性包含以下子值：

已安装

MediaSize

MediaColor

容量

级别

### <a name="span-idinstalledspanspan-idinstalledspan-installed"></a><span id="installed"></span><span id="INSTALLED"></span> 安装

架构路径：\\Printer.Layout.InputBins。\[TrayName\]： 安装

节点类型： 值

数据类型： BIDI\_BOOL

说明： 指示引用 bin \[TrayName\]设备上安装。 如果 **，则返回 TRUE**，bin 设备上安装了; 如果**FALSE**，bin 未安装在设备上。

### <a name="span-idmediasizespanspan-idmediasizespan-mediasize"></a><span id="mediasize"></span><span id="MEDIASIZE"></span> MediaSize

架构路径：\\Printer.Layout.InputBins。\[TrayName\]: MediaSize

节点类型： 值

数据类型： BIDI\_字符串

说明： 当前引用输入 bin 中有可用的介质的大小。 值应符合 IEEE-连接到它 PWG 标准 5101.1 2001-介质进行标准化名称。
允许以下值： na\_法律\_8.5x14in

na\_letter\_8.5x11in

iso\_a4\_210x297mm

iso\_c5\_162x229mm

iso\_dl\_110x220mm

jis\_b4\_257x364mm

### <a name="span-idmediatypespanspan-idmediatypespan-mediatype"></a><span id="mediatype"></span><span id="MEDIATYPE"></span> MediaType

架构路径：\\Printer.Layout.InputBins。\[TrayName\]： 媒体类型

节点类型： 值

数据类型： BIDI\_字符串

说明： 当前引用输入 bin 中有可用的媒体类型。 值应符合 IEEE-连接到它 PWG 标准 5101.1 2001-介质进行标准化名称。
允许以下值： 卡

信封

labels

照片

信纸

stationery-inkjet

透明度

其他

### <a name="span-idmediacolorspanspan-idmediacolorspan-mediacolor"></a><span id="mediacolor"></span><span id="MEDIACOLOR"></span> MediaColor

架构路径：\\Printer.Layout.InputBins。\[TrayName\]: MediaColor

节点类型： 值

数据类型： BIDI\_字符串

说明： 当前引用输入 bin 中有可用的介质的颜色。 值应符合 IEEE-连接到它 PWG 标准 5101.1 2001-介质进行标准化名称。
允许以下值： 白色

粉色

黄色

爱好者

金黄色

蓝色

绿色

红色

灰色

象牙塔

橙色

no-color

unknown

### <a name="span-idfeeddirectionspanspan-idfeeddirectionspan-feeddirection"></a><span id="feeddirection"></span><span id="FEEDDIRECTION"></span> FeedDirection

架构路径：\\Printer.Layout.InputBins。\[TrayName\]: FeedDirection

节点类型： 值

数据类型： BIDI\_字符串

说明： 指示在纸张的哪一边首先在当前引用的送纸器中输入的媒体路径，并且必须是以下值之一：

LongEdgeFirst

ShortEdgeFirst

### <a name="span-idcapacityspanspan-idcapacityspan-capacity"></a><span id="capacity"></span><span id="CAPACITY"></span> 容量

架构路径：\\Printer.Layout.InputBins。\[TrayName\]： 容量

节点类型： 值

数据类型： BIDI\_INT

说明： 中表的当前引用的送纸器的容量。

### <a name="span-idlevelspanspan-idlevelspan-level"></a><span id="level"></span><span id="LEVEL"></span> 级别

架构路径：\\Printer.Layout.InputBins。\[TrayName\]： 级别

节点类型： 值

数据类型： BIDI\_INT

说明： 的当前引用的送纸器，以百分比表示的剩余容量。 完整的送纸器必须值为 100，同时为空的任务栏的值为 0。 如果级别不是可衡量的则返回值为-1 （表示未知的级别）。

 

 




