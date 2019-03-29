---
title: NTSC 和隔行扫描数据
description: NTSC 和隔行扫描数据
ms.assetid: 216b6219-aeb8-4e8a-8ac4-cd4d25a93e13
keywords:
- 交错视频 WDK 的视频端口扩展
- DirectX VPE 支持 WDK DirectDraw，交错视频
- 绘制 VPEs WDK DirectDraw，交错视频
- DirectDraw VPEs WDK Windows 2000 显示，交错视频
- 视频端口扩展 WDK DirectDraw，交错视频
- VPEs WDK DirectDraw 隔行扫描视频
- NTSC WDK 的视频端口扩展
- 扫描行 WDK 的视频端口扩展
- 帧 WDK 的视频端口扩展
- 国家电视系统委员会 WDK VPEs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45809ce0d73a3470c0572234fa834bace8850e21
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576143"
---
# <a name="ntsc-and-interlaced-data"></a>NTSC 和隔行扫描数据


## <span id="ddk_ntsc_and_interlaced_data_gg"></span><span id="DDK_NTSC_AND_INTERLACED_DATA_GG"></span>


国家电视系统委员会 (NTSC) 标准提供了一系列的每秒的游戏如果在 59.94 交错字段，每部分都由 1/59.94 的第二个。 扫描线偶数字段之间的奇数的字段的扫描行在论据在空间上的中间。 但是，由于电视监视器荧光持久性，两个字段是永远不会显示电视屏幕上一次。 在查看器始终会看到甚至字段或奇数的字段，但永远不会同时。

一个*帧*NTSC 是完全不相关的两个顺序字段任意分组。 也就是说，在帧中的第一个字段是没有更多相关的同一框架中的第二个字段大于到上一帧中的第二个字段。 阶段替换行 (PAL) 格式和顺序的颜色与内存 (SECAM) 标准的工作方式与在每秒约 50 个字段。

如果视频包含高动态内容，奇数字段中的数据可能不同于，即使字段中。 因为您永远不会查看时这两个字段在同一时间，并密切关注执行很好地集成数据，这不会出现问题导致在电视监视器上。 计算机上，但是，此交错的数据通常是交错到单个缓冲区，然后使用渐进式扫描显示。 这意味着在同时，可能性较大 motion 项目的两个字段都可见。

将放入到数字视频光盘 (DVD) 上的视频，然后重播的过程很复杂。 通常情况下，对源材料放在磁盘上创建的电视节目，以便每个框架都具有交错的两个字段。 电影惊喜 24 帧每秒 (fps)，但是，必须转换为每秒与电视兼容的游戏如果在 59.94 字段。

 

 





