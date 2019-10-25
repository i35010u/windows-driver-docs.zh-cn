---
title: 基元绘制和状态更改
description: 基元绘制和状态更改
ms.assetid: 01eba14d-234e-48f5-9116-47760dfdae0e
keywords:
- Direct3D WDK Windows 2000 显示，基元绘图
- Direct3D WDK Windows 2000 显示，状态更改
- 状态 WDK Direct3D
- 基元绘图 WDK Direct3D
- D3dDrawPrimitives2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a015433ab537a58efd550139dbb1895c94d9851
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829702"
---
# <a name="primitive-drawing-and-state-changes"></a>基元绘制和状态更改


## <span id="ddk_primitive_drawing_and_state_changes_gg"></span><span id="DDK_PRIMITIVE_DRAWING_AND_STATE_CHANGES_GG"></span>


所有 Microsoft Direct3D 图形基元和状态更改都将传递到命令和顶点缓冲区中的[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)回调。 驱动程序必须分析这些缓冲区并处理所有绘图和状态更改请求。

以下部分介绍了命令和顶点缓冲区的布局，并说明了驱动程序应如何处理它们：

[命令和顶点缓冲区](command-and-vertex-buffers.md)

[Direct3D 命令缓冲区](direct3d-command-buffers.md)

[Direct3D 顶点缓冲区](direct3d-vertex-buffers.md)

[加速状态管理](accelerated-state-management.md)

 

 





