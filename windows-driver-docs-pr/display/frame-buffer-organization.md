---
title: 帧缓冲区组织
description: 帧缓冲区组织
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，视频解码
- 视频加速 WDK DirectX，视频解码
- VA WDK DirectX，视频解码
- 解码视频 WDK DirectX VA，帧缓冲区组织
- 视频解码 WDK DirectX VA，帧缓冲区组织
- 帧缓冲区组织 WDK DirectX VA
- 缓冲 WDK DirectX VA
- 预测块 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46fae9f1a207e826f1ab2d1d07d8128620b5c1c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799687"
---
# <a name="frame-buffer-organization"></a>帧缓冲区组织


## <span id="ddk_frame_buffer_organization_gg"></span><span id="DDK_FRAME_BUFFER_ORGANIZATION_GG"></span>


假定所有图片缓冲区都包含按 MPEG-2 视频规范 (示例位置指定为帧坐标) 中所述的框架组织的缓冲区。

可以使用特定于实现的转换层转换预测块，而不会丢失 (请参阅帧坐标到字段坐标中描述的有 *损压缩*) 。 例如，单个帧运动预测可以分为两个单独的宏块预测。

三个视频组件通道 (Y，Cb，Cr) 使用为 DirectX VA 定义的接口解码。  (Cb，Cr) 的两个色度组件的运动向量派生自 (Y) 为亮度组件发送的那些组件。 加速器负责将这些运动矢量转换为可使用的不同坐标系统。

下图显示了如何在主机和加速器中实现视频数据缓冲。

![阐释主机和加速器系统中视频数据缓冲的示意图](images/hostaccsys.png)

 

 





