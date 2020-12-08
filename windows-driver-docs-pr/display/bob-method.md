---
title: Bob 方法
description: Bob 方法
keywords:
- DirectX VPE 支持 WDK DirectDraw，并显示隔行扫描视频
- 绘制 VPEs WDK DirectDraw 并显示交错视频
- DirectDraw VPEs WDK Windows 2000 显示，显示交错视频
- 视频端口扩展 WDK DirectDraw，显示交错视频
- VPEs WDK DirectDraw，显示交错视频
- 显示隔行扫描视频
- 交错视频显示 WDK 视频端口扩展
- bob WDK DirectDraw
- 取消隔行扫描 WDK 视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc63d593559c02892be8c33363518d06ecae1950
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810425"
---
# <a name="bob-method"></a>Bob 方法


## <span id="ddk_bob_method_gg"></span><span id="DDK_BOB_METHOD_GG"></span>


显示数据的 bob 方法分别显示每个字段 (类似于) 使用叠加的电视。 生成的图像为正常高度的一半，因此在垂直方向使用内插叠加拉伸时，必须以垂直方向缩放200%。 但是，如果这是所有 bob 算法，则生成的图像将抖动和下降，因为奇数字段和偶数字段偏移一行。 如果使用插值来执行垂直拉伸，则在奇数字段上将一行添加到覆盖开始地址可以解决此问题。

Bob 方法生成 60 (NTSC) 每秒渐进帧，并保留来自交错源的所有临时信息。 如果视频是使用视频摄像机创建的，并且图像包含运动，则 bob 是渐进式监视器的最佳低成本显示流程。 Bob 方法适用于交错视频数据的所有源，但编织方法可产生更锐利的图像。

默认情况下，DirectShow 使用 bob 方法来更正隔行扫描。

 

 





