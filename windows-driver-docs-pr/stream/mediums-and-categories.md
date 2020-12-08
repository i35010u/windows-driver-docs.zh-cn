---
title: 媒体和类别
description: 媒体和类别
keywords:
- 视频捕获 WDK AVStream，媒体
- 捕获视频 WDK AVStream，媒体
- 视频捕获 WDK AVStream，流类别
- 捕获视频 WDK AVStream，流类别
- 标识 pin 主要用途
- 流类别 WDK 视频捕获
- 媒体 WDK 视频捕获
- 固定连接 WDK 视频捕获
ms.date: 06/18/2020
ms.localizationpriority: medium
ms.openlocfilehash: d5f170a05e8ca098a5d79d2d19f97b5058f62e29
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793337"
---
# <a name="mediums-and-categories"></a>媒体和类别

传统上，Microsoft DirectShow 流仅由其 [媒体类型](/previous-versions//ms787271(v=vs.85))标识。 虽然这对于呈现简单的筛选器图形来说是足够的，但对于反映硬件拓扑的更复杂的图形和图形，需要更多的信息以进行正确的图形生成。 为了使筛选器图生成正确地识别和连接 pin，视频捕获微型驱动程序指定其 pin 所属的流类别以及媒体。

流类别是用于标识 pin 的主要目的的一种方法。 例如，捕获筛选器可以具有两个每个 pin 支持相同 MediaTypes 的输出插针。 如果筛选器提供某个 pin 的优先级，则可以将较高优先级的 pin 分配给捕获流类别 (PINNAME \_ 视频 \_ 捕获) ，并将较低优先级的 pin 分配到预览流类别 (PINNAME \_ 视频 \_ 预览) 。

媒体是一种方法，可确保两个插针在单独的筛选器上的连接，例如电视调谐器筛选器上的模拟音频输出插针 (支持电视音频) ，以及电视音频筛选器上的电视音频输入插针。 考虑中型的一种方法是，它标识一个滤镜的输出插针与另一个滤镜的输入插针之间的一条线。

DirectShow 图形生成器接口（ **IFilterMapper2** 和 **ICaptureGraphBuilder**）使用这些方法来基于媒体和流类别构造筛选器关系图。
