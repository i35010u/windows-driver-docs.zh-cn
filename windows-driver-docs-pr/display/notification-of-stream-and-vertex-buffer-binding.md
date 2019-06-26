---
title: 流和顶点缓冲区绑定通知
description: 流和顶点缓冲区绑定通知
ms.assetid: 9ab9727f-053d-404b-95cc-ffd64fde7997
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多个顶点流
- 多个顶点流式传输 WDK DirectX 8.0
- 顶点多个流 WDK DirectX 8.0
- 顶点缓冲区 WDK DirectX 8.0
- 绑定到顶点的流缓冲区 WDK DirectX 8.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27a8caba2ef2f8b90ec4329ed72dbbbb2b8401a9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67372800"
---
# <a name="notification-of-stream-and-vertex-buffer-binding"></a>流和顶点缓冲区绑定通知


## <span id="ddk_notification_of_stream_vertex_buffer_binding_gg"></span><span id="DDK_NOTIFICATION_OF_STREAM_VERTEX_BUFFER_BINDING_GG"></span>


驱动程序通知的绑定到通过新的 DP2 令牌 D3DDP2OP 的特定流的顶点缓冲区\_SETSTREAMSOURCE，及其关联的 HAL 数据结构， [ **D3DHAL\_DP2SETSTREAMSOURCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3dhal/ns-d3dhal-_d3dhal_dp2setstreamsource).

 

 





