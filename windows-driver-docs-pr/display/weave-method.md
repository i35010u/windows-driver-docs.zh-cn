---
title: Weave 方法
description: Weave 方法
ms.assetid: d35a08b6-7221-4e1c-895f-446f23096519
keywords:
- DirectX VPE 支持 WDK DirectDraw，显示交错的视频
- 绘制 VPEs WDK DirectDraw，显示交错视频
- DirectDraw VPEs WDK Windows 2000 显示，显示交错的视频
- 视频端口扩展 WDK DirectDraw，显示交错的视频
- VPEs WDK DirectDraw，显示交错的视频
- 显示交错的视频
- 交错的视频显示 WDK 的视频端口扩展
- 将 WDK DirectDraw
- 取消隔行扫描 WDK 的视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 803c33ccecd4a3be5db9938237c82d29cb1d23e4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63391177"
---
# <a name="weave-method"></a>Weave 方法


## <span id="ddk_weave_method_gg"></span><span id="DDK_WEAVE_METHOD_GG"></span>


编织物方法使用硬件视频端口到覆盖面交错交错的字段显示数据，然后在同一时间显示这两个字段。 如果这是所有 weave 实现算法一样，但是，motion 项目会显示。 编织物算法也依赖于 MPEG 驱动程序，以识别 3:2 模式，然后撤消它在内核模式视频传输中使用函数。 内核模式视频传输可能会导致硬件放弃重复的字段，从而导致所有字段对来自同一帧的视频端口。 就像它最初使用电影采样，则结果为全帧视频显示每秒 24 帧的速率。

由两个或三个字段的 NTSC 信号表示为每个源电影帧。 这可以作为两个组成一个帧的一个字段来看待。 每个序列的四个电影帧转换为五个电视帧。 A、 B、 C 和 D 的电影帧成为五个电视帧中的字段模式 AA、 BB、 BC、 CD、 和 dd。 当重复\_字段标志用于编码 MPEG 流中的此模式，MPEG 数据有效负载包含只有四个帧，但保留所有五个电视帧的字段顺序。

编织物方法会生成 24 渐进式每秒帧数并保留交错源中的完整垂直分辨率。 如果视频根据电影胶片使用 3:2 下拉列表中，创建或不包含任何动作，编织物是渐进式监视器的最经济实惠显示进程。

 

 





