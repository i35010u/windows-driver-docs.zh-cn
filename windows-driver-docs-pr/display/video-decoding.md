---
title: 视频解码
description: 视频解码
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，视频解码
- 视频加速 WDK DirectX，视频解码
- VA WDK DirectX，视频解码
- 解码视频 WDK DirectX VA，关于解码视频
- 视频解码 WDK DirectX VA，关于解码视频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c46995fa8f737131b28b89087ed1097c9ee7bdf4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802515"
---
# <a name="video-decoding"></a>视频解码


## <span id="ddk_video_decoding_gg"></span><span id="DDK_VIDEO_DECODING_GG"></span>


DirectX VA 允许将视频解码过程中的一个或多个阶段划分为 *主机 CPU* 和视频硬件加速器。 该快捷键执行 [运动补偿预测](motion-compensated-prediction.md) (MCP) ，还可以执行反离散的余弦转换 (IDCT) 和可变长度解码， (解码过程的 VLD) 阶段。

DirectX VA API 对单个视频流进行解码。 支持多个视频流需要为每个视频流提供单独的 DirectX VA 会话 (例如，一对用于在筛选器图形) 操作中使用的视频解码器和加速驱动程序的输出和输入插针。 有关筛选器关系图的详细信息，请参阅 [KS 微型驱动程序体系结构](../stream/ks-minidriver-architecture.md)。

 

