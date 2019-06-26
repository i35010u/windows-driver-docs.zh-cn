---
title: 基元绘制和状态更改
description: 基元绘制和状态更改
ms.assetid: 01eba14d-234e-48f5-9116-47760dfdae0e
keywords:
- Direct3D WDK Windows 2000 显示基元绘制
- Direct3D WDK Windows 2000 显示状态更改
- 指出 WDK Direct3D
- 基元绘制 WDK Direct3D
- D3dDrawPrimitives2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 828ca3e214d925e2a153d944cc43a6d1f4460f04
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363737"
---
# <a name="primitive-drawing-and-state-changes"></a>基元绘制和状态更改


## <span id="ddk_primitive_drawing_and_state_changes_gg"></span><span id="DDK_PRIMITIVE_DRAWING_AND_STATE_CHANGES_GG"></span>


所有 Microsoft Direct3D 图形基元和状态更改都传递给[ **D3dDrawPrimitives2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)命令和顶点缓冲区中的回调。 该驱动程序必须解析这些缓冲区和处理所有绘图和状态更改请求。

以下各节介绍的命令和顶点缓冲区布局，以及驱动程序应如何处理它们：

[命令和顶点缓冲区](command-and-vertex-buffers.md)

[Direct3D 命令缓冲区](direct3d-command-buffers.md)

[Direct3D 顶点缓冲区](direct3d-vertex-buffers.md)

[加速状态管理](accelerated-state-management.md)

 

 





