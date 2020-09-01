---
title: 流和顶点缓冲区绑定通知
description: 流和顶点缓冲区绑定通知
ms.assetid: 9ab9727f-053d-404b-95cc-ffd64fde7997
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，多个顶点流
- 多个顶点流 WDK DirectX 8。0
- 顶点多流 WDK DirectX 8。0
- 顶点缓冲 WDK DirectX 8。0
- 流绑定到顶点缓冲区 WDK DirectX 8。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9abc133e9e770681eb25fefdc58f1201a070a6b
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067312"
---
# <a name="notification-of-stream-and-vertex-buffer-binding"></a>流和顶点缓冲区绑定通知


## <span id="ddk_notification_of_stream_vertex_buffer_binding_gg"></span><span id="DDK_NOTIFICATION_OF_STREAM_VERTEX_BUFFER_BINDING_GG"></span>


通过新的 DP2 令牌、D3DDP2OP \_ SETSTREAMSOURCE 及其关联的 HAL 数据结构 [**D3DHAL \_ DP2SETSTREAMSOURCE**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2setstreamsource)，通知驱动程序将顶点缓冲区绑定到特定流。

 

