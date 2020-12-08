---
title: 流和顶点缓冲区绑定通知
description: 流和顶点缓冲区绑定通知
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多个顶点流
- 多个顶点流 WDK DirectX 8。0
- 顶点多流 WDK DirectX 8。0
- 顶点缓冲 WDK DirectX 8。0
- 流绑定到顶点缓冲区 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 923680d41d01d9318ce2ef2b38d9502fe3212386
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840369"
---
# <a name="notification-of-stream-and-vertex-buffer-binding"></a>流和顶点缓冲区绑定通知


## <span id="ddk_notification_of_stream_vertex_buffer_binding_gg"></span><span id="DDK_NOTIFICATION_OF_STREAM_VERTEX_BUFFER_BINDING_GG"></span>


通过新的 DP2 令牌、D3DDP2OP \_ SETSTREAMSOURCE 及其关联的 HAL 数据结构 [**D3DHAL \_ DP2SETSTREAMSOURCE**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setstreamsource)，通知驱动程序将顶点缓冲区绑定到特定流。

 

