---
title: NTSC/PAL 转换
description: NTSC/PAL 转换
keywords:
- 隔行扫描视频 WDK 视频端口扩展
- DirectX VPE 支持 WDK DirectDraw、隔行扫描视频
- 绘制 VPEs WDK DirectDraw，隔行扫描视频
- DirectDraw VPEs WDK Windows 2000 显示，隔行扫描视频
- 视频端口扩展 WDK DirectDraw，隔行扫描视频
- VPEs WDK DirectDraw，隔行扫描视频
- NTSC/PAL WDK 视频端口扩展
- 将 NTSC 转换为 PAL
- 3 2 下拉 WDK 视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0393579ff4dea67f71c365dbc8d600675249a0ed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792969"
---
# <a name="ntscpal-conversion"></a>NTSC/PAL 转换


## <span id="ddk_ntsc_pal_conversion_gg"></span><span id="DDK_NTSC_PAL_CONVERSION_GG"></span>


从 NTSC 到 PAL 的转换是通过快速播放电影来完成的，即 25 fps。 两个顺序字段是从同一个帧创建的，并显示 1/50 秒。 通过使用名为 *3:2* 的过程重复每第五个视频字段，实现从 PAL 到 NTSC 的转换。 第一个胶片帧用于创建两个视频字段，然后使用第二个胶片帧创建三个视频字段。 此过程将重复进行，以便将奇数甚至偶数个字段按顺序进行发送。

因此，从胶卷创建的隔行扫描视频包含字段对。 但不同于标准电视信号，其中每个字段分别为 1/60th 或 1/50/50。其中许多字段对包含同一胶片帧中的数据。 同时显示这些字段对不会生成任何项目，并且提供比电视监视器更好的结果。 但是，不在同一帧中的任何字段对将分别为1/24，并且可能会产生更多项目。

编码隔行扫描视频时，将设置一个标志来指示应如何对流进行解码。 此信息应该足以解码并以最佳方式显示已解码的图片，因为用于 DVD 或 DSS 的 MPEG-2 或 NTSC 解码器输出的理论上始终为50或60隔行扫描字段。 但是，较旧的电影和一些较新的电影通常会在标志节奏中产生中断，尤其是在胶片卷轴的转变点上。 这需要用于标识此类渐进式内容的方法，以便选择适当的方法来显示每帧帧的信息。

 

 





