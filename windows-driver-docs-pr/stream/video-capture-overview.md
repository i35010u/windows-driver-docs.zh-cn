---
title: 视频捕获概述
description: 视频捕获概述
ms.assetid: 3f299905-beab-48e2-b5c9-9850452115c6
keywords:
- 有关视频捕获的视频捕获 WDK AVStream
- 捕获有关视频捕获的视频 WDK AVStream
- 视频捕获 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c2b6819daba4ab50acccf93fe2047ea7f40c7046
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554986"
---
# <a name="video-capture-overview"></a>视频捕获概述


视频捕获微型驱动程序与 AVStream 的 Stream 类任一接口来控制生成的视频数据，以及辅助数据，例如电视音频流的或作为主要的硬件设备 / 调频调谐器功能。 供应商编写到视频捕获微型驱动程序：

-   从数字和模拟视频源，例如，IEEE 1394、 USB、 S-视频、 压缩和未压缩视频流和 RCA 插孔视频中捕获。

-   捕获垂直遮蔽的间隔 (VBI) 数据。

-   捕获辅助数据流，如电视的音频或 AM / 调频调谐器音频。

-   捕获时间码。

-   控制视频端口和捕获从视频端口的流视频。

-   控制与视频流，例如电视/广播调谐器，信号路由设备 （纵横制）、 电视音频控件和视频压缩程序关联的设备。

-   控制摄像头属性，如缩放、 平移和焦点。

-   控制视频属性，如色调、 饱和度、 亮度和清晰度。

-   提供了 WDM 流式处理 （适用于内核模式） 和 （适用于用户模式） 的 DirectShow 兼容性。

 

 




