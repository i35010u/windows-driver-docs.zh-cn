---
title: 隐藏式字幕流
description: 隐藏式字幕流
ms.assetid: ee6cfac6-c532-4e73-81b2-ee767d2d6a4d
keywords:
- 关闭隐藏字幕流 WDK DVD 解码器
- 图片 WDK DVD 解码器的组
- GOP WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f2f062bd8a353e7c63884b35ab1a2cfa7e14aa0a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568288"
---
# <a name="closed-captioning-streams"></a>隐藏式字幕流





支持为隐藏字幕是必需的。 DVD 解码器微型驱动程序必须提供 Microsoft 行 21 解码器筛选器已关闭隐藏字幕的信息。 实现可能不是简单地解码 MPEG2 解码器内的已关闭隐藏式字幕信息并将其添加到视频流。 DVD 解码器微型驱动程序必须显示关闭字幕 pin 为输出插针。 打开流后，DVD 解码器微型驱动程序将收到 SRB\_读取\_流上的数据请求。 DVD 解码器微型驱动程序这些请求排队，直到关闭的隐藏式字幕数据可用。

在视频流中处理一组 (gop) 启动代码时，DVD 解码器微型驱动程序查找用户数据 （已关闭隐藏式字幕信息），并返回上关闭字幕使用一个流请求的块 (Srb) 存在该信息流队列。 所有数据的不连续性和格式块更改应从视频 pin 都传播到已关闭的隐藏式字幕 pin。

 

 




