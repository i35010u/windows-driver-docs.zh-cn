---
title: 渐进式扫描监视器和交错的数据
description: 渐进式扫描监视器和交错的数据
ms.assetid: 324d8b1f-5b7d-46b6-854a-e93b10db24e5
keywords:
- 交错视频 WDK 的视频端口扩展
- DirectX VPE 支持 WDK DirectDraw，交错视频
- 绘制 VPEs WDK DirectDraw，交错视频
- DirectDraw VPEs WDK Windows 2000 显示，交错视频
- 视频端口扩展 WDK DirectDraw，交错视频
- VPEs WDK DirectDraw 隔行扫描视频
- DirectX VPE 支持 WDK DirectDraw，proscan 监视器
- 绘制 VPEs WDK DirectDraw，proscan 监视器
- DirectDraw VPEs WDK Windows 2000 显示，proscan 监视器
- 视频端口扩展 WDK DirectDraw，proscan 监视器
- VPEs WDK DirectDraw，proscan 监视器
- proscan 监视器 WDK 的视频端口扩展
- 渐进式扫描监控在 WDK 的视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51817f2b58d40677b65871db843fb92c910334e8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540618"
---
# <a name="progressive-scan-monitors-and-interleaved-data"></a>渐进式扫描监视器和交错的数据


## <span id="ddk_progressive_scan_monitors_and_interleaved_data_gg"></span><span id="DDK_PROGRESSIVE_SCAN_MONITORS_AND_INTERLEAVED_DATA_GG"></span>


作为框架在 proscan 监视器上显示的行-即，显示第 1 行，然后行 2，则行 3，等等。 典型的电视设置显示*2:1 光栅*--即，它显示一个帧的第一个字段上的奇数行，然后偶数行上显示的帧的第二个字段。 Proscan 监视器上显示之前，必须先处理用于在电视上播放任何材料。

 

 





