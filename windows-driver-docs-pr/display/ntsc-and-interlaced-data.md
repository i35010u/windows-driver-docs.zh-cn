---
title: NTSC 和隔行扫描数据
description: NTSC 和隔行扫描数据
keywords:
- 隔行扫描视频 WDK 视频端口扩展
- DirectX VPE 支持 WDK DirectDraw、隔行扫描视频
- 绘制 VPEs WDK DirectDraw，隔行扫描视频
- DirectDraw VPEs WDK Windows 2000 显示，隔行扫描视频
- 视频端口扩展 WDK DirectDraw，隔行扫描视频
- VPEs WDK DirectDraw，隔行扫描视频
- NTSC WDK 视频端口扩展
- 扫描线条 WDK 视频端口扩展
- 帧 WDK 视频端口扩展
- 国家电视系统委员会 WDK VPEs
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2706d3a2f5f8a6871c3145f20a836f1ae465283c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792975"
---
# <a name="ntsc-and-interlaced-data"></a>NTSC 和隔行扫描数据


## <span id="ddk_ntsc_and_interlaced_data_gg"></span><span id="DDK_NTSC_AND_INTERLACED_DATA_GG"></span>


国内电视系统委员会 (NTSC) standard 提供一系列59.94 交错字段，每秒由 1/59.94 隔开。 偶数字段的扫描行在奇号字段的扫描行之间秋季间隔。 不过，由于电视显示器的 phosphor 持久性，两个字段绝不会同时显示在电视屏幕上。 查看器始终会看到偶数字段或奇数字段，但绝不会同时出现这两种情况。

NTSC 中的 *帧* 是完全不相关的两个连续字段的任意分组。 也就是说，框架中的第一个字段与前一帧中的第二个字段相比，与第二个字段不在同一帧中。 阶段替换行 (PAL) 格式， (SECAM) 标准工作的有序颜色，每秒大约50个字段。

如果视频包含高动作内容，则奇数字段中的数据可能不同于偶数字段中的数据。 这不会导致电视显示器上出现问题，因为你不会同时查看这两个字段，并且眼就会在集成数据的情况下执行良好的任务。 但是，在计算机上，此交错数据通常交错为单个缓冲区，然后使用渐进式扫描来显示。 这意味着，这两个字段在同一时间可见，因此可能会出现运动项目。

将视频放入数字视频光盘 (DVD) ，然后将其重播的过程很复杂。 通常，在磁盘上放置的源材料是为电视创建的，因此每个帧都有两个交错字段。 每秒24帧的胶片快照 (fps) ，但是，每秒必须转换为59.94 个字段，才能兼容电视节目。

 

 





