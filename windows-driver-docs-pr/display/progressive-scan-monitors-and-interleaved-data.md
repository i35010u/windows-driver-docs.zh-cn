---
title: 逐行扫描监视器和隔行扫描数据
description: 逐行扫描监视器和隔行扫描数据
keywords:
- 隔行扫描视频 WDK 视频端口扩展
- DirectX VPE 支持 WDK DirectDraw、隔行扫描视频
- 绘制 VPEs WDK DirectDraw，隔行扫描视频
- DirectDraw VPEs WDK Windows 2000 显示，隔行扫描视频
- 视频端口扩展 WDK DirectDraw，隔行扫描视频
- VPEs WDK DirectDraw，隔行扫描视频
- DirectX VPE 支持 WDK DirectDraw，proscan 监视器
- 绘制 VPEs WDK DirectDraw，proscan 监视器
- DirectDraw VPEs WDK Windows 2000 显示，proscan 监视器
- 视频端口扩展 WDK DirectDraw，proscan 监视器
- VPEs WDK DirectDraw，proscan 监视器
- proscan 监视 WDK 视频端口扩展
- 渐进式扫描监视 WDK 视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0dea6fd2aa8d0f76f92fe88c1008bb990e116c6b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840995"
---
# <a name="progressive-scan-monitors-and-interleaved-data"></a>逐行扫描监视器和隔行扫描数据


## <span id="ddk_progressive_scan_monitors_and_interleaved_data_gg"></span><span id="DDK_PROGRESSIVE_SCAN_MONITORS_AND_INTERLEAVED_DATA_GG"></span>


在 proscan 监视器上，行显示为一个帧-即，显示第1行，第2行，第3行，依此类推。 典型的电视节目会显示一个 *2:1 的光栅* ，也就是说，它将在奇数行上显示某个帧的第一个字段，然后在偶数行上显示该框架的第二个字段。 任何要在电视上播放的材料，都必须在 proscan 显示器上进行处理。

 

 





