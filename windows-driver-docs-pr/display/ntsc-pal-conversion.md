---
title: NTSC/PAL 转换
description: NTSC/PAL 转换
ms.assetid: 2ae22ebd-e75a-4f9c-b50e-d0ddfe05d987
keywords:
- 交错视频 WDK 的视频端口扩展
- DirectX VPE 支持 WDK DirectDraw，交错视频
- 绘制 VPEs WDK DirectDraw，交错视频
- DirectDraw VPEs WDK Windows 2000 显示，交错视频
- 视频端口扩展 WDK DirectDraw，交错视频
- VPEs WDK DirectDraw 隔行扫描视频
- NTSC/PAL WDK 的视频端口扩展
- 转换 NTSC 或 PAL
- 3 2 的下拉式 WDK 的视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 284121130ec98830394f073cbcf4acdff898a88b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384087"
---
# <a name="ntscpal-conversion"></a>NTSC/PAL 转换


## <span id="ddk_ntsc_pal_conversion_gg"></span><span id="DDK_NTSC_PAL_CONVERSION_GG"></span>


只需为 25 fps 播放电影快速--通过从 NTSC 或 PAL 的转换。 两个顺序字段都从同一框架创建并显示 1/秒间隔的第 50。 通过重复调用进程与每个第五个视频字段进行转换从 PAL 到 NTSC *3:2 下拉方式*。 第一个的电影帧用于创建两个视频字段，然后第二个电影帧用于创建三个视频的字段。 以便按顺序 Ao Ae Ao 是 Bo Ce 共同 Ce 发送奇数和偶数字段重复此过程。

因此，创建从电影胶片交错的视频包含字段的对。 但与标准电视信号，其中每个字段为 1/60th 或 1/秒间隔; 的第 50许多这些字段对包含电影胶片的同一个帧中的数据。 在同一时间显示这些字段对不会生成任何项目，并提供比电视监视器更好的结果执行操作。 但是，不能从同一帧任何字段对将秒间隔的 1/24，并且可能无法生成多个项目。

交错的视频进行编码，将重新设置标志以指示应如何解码流。 这应该是足够的信息进行解码，并以最佳方式显示的已解码的图片，因为 mpeg-2 或 DVD 或 DSS NTSC 解码器的输出始终从理论上讲是每秒 50 或 60 交错的字段。 但是，较旧的电影和某些较新的影片通常具有一个分行符标志节奏，尤其是在电影卷盘转变点中。 若要选择适当的方法，用于显示有关帧的帧来信息识别这种渐进式内容这需要一种方法。

 

 





