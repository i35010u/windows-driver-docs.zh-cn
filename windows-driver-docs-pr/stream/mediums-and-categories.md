---
title: 媒体和类别
description: 媒体和类别
ms.assetid: 2bc83ce6-7f79-44e7-a0fb-7b9f56771730
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
ms.openlocfilehash: 52bd0fa781a9cea025f5384253641053d4eeb8c5
ms.sourcegitcommit: 31fa7dbbcd051d7ec1ea3e05a4c0340af9d3b8a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2020
ms.locfileid: "85073436"
---
# <a name="mediums-and-categories"></a>媒体和类别

传统上，Microsoft DirectShow 流仅由其[媒体类型](https://docs.microsoft.com/previous-versions//ms787271(v=vs.85))标识。 虽然这对于呈现简单的筛选器图形来说是足够的，但对于反映硬件拓扑的更复杂的图形和图形，需要更多的信息以进行正确的图形生成。 为了使筛选器图生成正确地识别和连接 pin，视频捕获微型驱动程序指定其 pin 所属的流类别以及媒体。

流类别是用于标识 pin 的主要目的的一种方法。 例如，捕获筛选器可以具有两个每个 pin 支持相同 MediaTypes 的输出插针。 如果筛选器提供了某个 pin 的优先级，则可以将较高优先级的 pin 分配到 "捕获流" 类别（PINNAME \_ 视频 \_ 捕获），将较低优先级的 pin 分配到 "预览流" 类别（PINNAME \_ 视频 \_ 预览版）。

媒体是一种方法，用于确保两个 pin 在单独的筛选器上的连接，例如电视调谐器筛选器上的模拟音频输出插针（用于支持电视音频）和电视音频筛选器上的电视音频输入插针。 考虑中型的一种方法是，它标识一个滤镜的输出插针与另一个滤镜的输入插针之间的一条线。

DirectShow 图形生成器接口（ **IFilterMapper2**和**ICaptureGraphBuilder**）使用这些方法来基于媒体和流类别构造筛选器关系图。
