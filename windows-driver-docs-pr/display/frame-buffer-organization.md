---
title: 帧缓冲区组织
description: 帧缓冲区组织
ms.assetid: 2a9ce844-84c5-4517-acf7-c7e67a1e5e07
keywords:
- DirectX 视频加速 WDK Windows 2000 显示视频解码
- 视频加速 WDK DirectX，视频解码
- VA WDK DirectX，视频解码
- 解码视频 WDK DirectX va，因此帧缓冲区组织
- 视频解码 WDK DirectX va，因此帧缓冲区组织
- 帧缓冲区组织 WDK DirectX VA
- 缓冲 WDK DirectX VA
- 预测阻止 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: efe643a2130d6cb64058d4af53ca520b15130996
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544827"
---
# <a name="frame-buffer-organization"></a>帧缓冲区组织


## <span id="ddk_frame_buffer_organization_gg"></span><span id="DDK_FRAME_BUFFER_ORGANIZATION_GG"></span>


所有图片缓冲区都假定要让框架组织 mpeg-2 视频规范 （位置作为帧坐标，给出的示例） 中所述的缓冲区。

可以使用特定于实现的转换层将转换而不会丢失预测块 (请参阅*有损压缩*) 所述为字段坐标的帧坐标。 例如，单个帧运动预测可以分解为两个单独的、 顶部和下宏块部分预测。

三个视频组件通道 （Y、 Cb、 Cr） 为解码状态使用的 DirectX 弗吉尼亚定义的接口 两个色度组件 （Cb，Cr） 的动作矢量派生自这些发送亮度组件 (Y)。 快捷键将负责任何这些动作矢量转换到不同可能使用的坐标系统。

下图显示了如何视频数据缓冲中的主机和加速器实现。

![说明在主机和加速器系统中缓冲视频数据的关系图](images/hostaccsys.png)

 

 





