---
title: 隐藏式字幕流
description: 隐藏式字幕流
keywords:
- 隐藏式字幕流 WDK DVD 解码器
- 图片组 WDK DVD 解码器
- GOP WDK DVD 解码器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1bbac58fb8fbaa5ff156fefebe58ec53eec6f44
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788173"
---
# <a name="closed-captioning-streams"></a>隐藏式字幕流





需要支持隐藏式字幕。 DVD 解码器微型驱动程序必须提供 Microsoft line 21 解码器筛选器的隐藏式字幕信息。 实现可能不只是对 MPEG2 解码器内隐藏的字幕信息进行解码，而是将其添加到视频流中。 DVD 解码器微型驱动程序必须将隐藏式字幕 pin 作为输出插针提供。 打开流后，DVD 解码器微型驱动程序将 \_ \_ 在流上收到 SRB 的读取数据请求。 DVD 解码器微型驱动程序会将这些请求排队，直到隐藏的字幕数据可用。

当在视频流中处理 (GOP) "启动代码" 的一组图片时，DVD 解码器微型驱动程序将查找用户数据 (隐藏的字幕信息) 并使用 "隐藏式字幕流" 队列中的一个流请求块 (SRBs）返回该信息。 所有数据不连续性和格式块更改都应该从视频 pin 传播到隐藏式字幕 pin。

 

 




