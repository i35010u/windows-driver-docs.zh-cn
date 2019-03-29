---
title: 媒体和类别
description: 媒体和类别
ms.assetid: 2bc83ce6-7f79-44e7-a0fb-7b9f56771730
keywords:
- 视频捕获 WDK AVStream，介质
- 捕获视频 WDK AVStream，介质
- 视频捕获 WDK AVStream，流类别
- 捕获视频 WDK AVStream，流类别
- 标识 pin 主要用途
- 流类别 WDK 视频捕获
- 媒体 WDK 视频捕获
- pin 连接 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1d88fb8020a0acfacd71709ac20d2e3f7c967e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567811"
---
# <a name="mediums-and-categories"></a>媒体和类别


一直以来，Microsoft DirectShow 流已证实存在完全由其[媒体类型](https://go.microsoft.com/fwlink/p/?linkid=51458)。 尽管这足以用于呈现简单的筛选器关系图，更复杂的关系图和关系图，以反映硬件拓扑为正确的关系图构建需要其他信息。 若要启用筛选器关系图构建正确标识并连接插针，视频捕获微型驱动程序指定流类别属于他们的 pin，以及媒体。

Stream 类别是一种方法来标识 pin 的主要目的。 例如，使用捕获筛选器可以有两个输出插针，其中在每个插针上受支持的相同 MediaTypes。 在其中筛选器为优先级到其中一个球瓶的情况下，优先级较高的 pin 可以分配给捕获流类别 (PINNAME\_视频\_捕获)，以及到预览流类别 (PINNAME优先级较低的pin\_视频\_预览版)。

媒体是一种方法来确保两个插针上单独的筛选器之间的连接，如模拟音频输出插针上 （以支持电视音频） 的电视调谐器筛选器，以及电视音频输入插针上的电视音频筛选器。 一种方法可以看作是一种介质是它标识一个筛选器的输出插针和另一个筛选器输入插针之间以有线方式。

DirectShow 图形生成器接口**IFilterMapper2**并**ICaptureGraphBuilder**，使用这些方法来构造筛选器关系图基于媒体和流类别。

 

 




