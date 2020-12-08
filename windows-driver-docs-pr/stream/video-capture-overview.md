---
title: 视频捕获概述
description: 视频捕获概述
keywords:
- 视频捕获 WDK AVStream，关于视频捕获
- 捕获有关视频捕获的视频 WDK AVStream
- 视频捕获 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 611c76f997306b87092be530ab0c83ab632e6a37
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809807"
---
# <a name="video-capture-overview"></a>视频捕获概述


视频捕获微型驱动程序与 Stream 类接口的 AVStream 进行交互，以控制主要生成视频数据流流的硬件设备，以及辅助数据，如电视音频或 AM/调频调谐器功能。 供应商编写视频捕获微型驱动程序：

-   从数字和模拟视频源（如 IEEE 1394、USB、S-视频和 RCA 视频插孔）捕获压缩的未压缩视频流。

-   捕获垂直消隐间隔 (VBI) 数据。

-   捕获辅助数据流，如电视音频或 AM/调频调谐器音频。

-   捕获时间码。

-   控制视频端口并捕获视频端口流中的视频。

-   控制与视频流关联的设备，如电视/收音机调谐器、信号路由设备 (crossbars) 、电视音频控制和视频 compressors。

-   控制缩放、平移和焦点等照相机属性。

-   控制视频属性，如色调、饱和度、亮度和清晰度。

-   为内核模式提供 WDM 流式处理 () 和 DirectShow (，) 兼容性。

 

 




