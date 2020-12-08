---
title: 使用 VPE 显示隔行扫描视频
description: 使用 VPE 显示隔行扫描视频
keywords:
- DirectX VPE 支持 WDK DirectDraw，并显示隔行扫描视频
- 绘制 VPEs WDK DirectDraw 并显示交错视频
- DirectDraw VPEs WDK Windows 2000 显示，显示交错视频
- 视频端口扩展 WDK DirectDraw，显示交错视频
- VPEs WDK DirectDraw，显示交错视频
- 显示隔行扫描视频
- 交错视频显示 WDK 视频端口扩展
- 隔行扫描视频 WDK 视频端口扩展
- 取消隔行扫描 WDK 视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d23fdebde9444787f7b3eca2742df55e1637a86d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809215"
---
# <a name="displaying-interleaved-video-with-vpe"></a>使用 VPE 显示隔行扫描视频


## <span id="ddk_displaying_interleaved_video_with_vpe_gg"></span><span id="DDK_DISPLAYING_INTERLEAVED_VIDEO_WITH_VPE_GG"></span>


取消隔行扫描有许多方法。 当取消隔行扫描用于大大小的背投显示时，专业电视发生器使用诸如 line doublers 之类的设备，并在创建缩放和慢速动作序列时影响带有动作自适应筛选器的系统。

可以通过两种简单的方法在渐进式计算机监视器上显示交错： [bob](bob-method.md) 和 [编织](weave-method.md)。 出于简单起见，此处使用了这些术语，因为计算机和电视行业术语有所不同。

 

 





