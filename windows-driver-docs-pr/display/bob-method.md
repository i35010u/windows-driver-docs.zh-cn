---
title: Bob 方法
description: Bob 方法
ms.assetid: 3ef4ad25-fe62-4f80-8d0a-d21035d93c1f
keywords:
- DirectX VPE 支持 WDK DirectDraw，显示交错的视频
- 绘制 VPEs WDK DirectDraw，显示交错视频
- DirectDraw VPEs WDK Windows 2000 显示，显示交错的视频
- 视频端口扩展 WDK DirectDraw，显示交错的视频
- VPEs WDK DirectDraw，显示交错的视频
- 显示交错的视频
- 交错的视频显示 WDK 的视频端口扩展
- bob WDK DirectDraw
- 取消隔行扫描 WDK 的视频端口扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4eb7159560173e198ad8fea688a5a748636a72a5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533565"
---
# <a name="bob-method"></a>Bob 方法


## <span id="ddk_bob_method_gg"></span><span id="DDK_BOB_METHOD_GG"></span>


显示数据的 bob 方法分别显示每个字段 （类似于电视） 使用一个覆盖区。 生成的映像是普通的半高，因此它必须是在使用内插的覆盖拉伸的垂直方向的缩放的 200%。 但是，如果这是 bob 算法做的全部工作，生成的映像将抖动向上和向下因为奇数字段和甚至字段偏移的一行。 为覆盖起始地址的奇数个字段添加一个行解决了此问题，只要使用内插器执行垂直拉伸。

Bob 方法生成每秒 60 (NTSC) 渐进式帧，并保留交错源中的所有临时信息。 如果视频创建视频摄像机和映像包含动作，bob 是渐进式监视器的最佳的低成本显示进程。 Bob 方法适用于所有的交错视频数据源，但 weave 实现方法生成更鲜艳的图像。

默认情况下，DirectShow 纠正交错的显示使用 bob 方法。

 

 





