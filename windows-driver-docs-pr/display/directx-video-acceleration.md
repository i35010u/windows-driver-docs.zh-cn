---
title: DirectX 视频加速
description: DirectX 视频加速
keywords:
- DirectX 视频加速 WDK Windows 2000 显示
- 视频加速 WDK DirectX
- 运动补偿 WDK
- VA WDK DirectX
- 加速器 WDK DirectX
- 显示驱动程序模型 WDK Windows 2000，DirectX 视频加速
- Windows 2000 显示器驱动程序模型 WDK，DirectX 视频加速
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb7cb9a0c243b68905d26b0c76dd6fb5c27302ef
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809299"
---
# <a name="directx-video-acceleration"></a>DirectX 视频加速


## <span id="ddk_directx_video_acceleration_gg"></span><span id="DDK_DIRECTX_VIDEO_ACCELERATION_GG"></span>


本部分包含有关 Microsoft DirectX 视频加速 (DirectX VA) 的信息。 这是一种应用程序编程接口 (API) ，以及相应的 [运动补偿](motion-compensation.md) 设备驱动程序接口 (DDI) 以加速数字视频解码。 还提供了以下附加 DDIs 作为 DirectX VA 的一部分：

-   用于取消隔行扫描的 [取消隔行扫描 DDI](./deinterlace-ddi.md) 和视频内容的帧速率转换。

-   支持 ProcAmp 控制和后处理视频内容的 [PROCAMP DDI](./procamp-control-ddi.md) 。

-   用于保护视频内容的 [COPP DDI](sample-functions-for-copp.md) 。

为 Microsoft Windows XP Service Pack 1 (SP1) 和更高版本创建 DirectX VA 驱动程序的驱动程序编写器应使用 *dxva* 头文件。 其中包含用于视频加速和取消隔行扫描的结构和枚举，以及帧速率转换。

本节包括下列主题：

[DirectX VA 简介](introduction-to-directx-va.md)

[视频解码](video-decoding.md)

[反交错和帧速率转换](deinterlacing-and-frame-rate-conversion.md)

[ProcAmp 控制处理](procamp-control-processing.md)

[COPP 处理](copp-processing.md)

[DirectX VA 设备的示例代码](example-code-for-directx-va-devices.md)

[DirectX VA 数据流管理](directx-va-data-flow-management.md)

[DirectX VA 操作](directx-va-operations.md)

[定义加速器功能](defining-accelerator-capabilities.md)
