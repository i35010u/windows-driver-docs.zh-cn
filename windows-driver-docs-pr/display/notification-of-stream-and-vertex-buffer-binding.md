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
ms.openlocfilehash: 8ca8485f65e7c74ff0ef3e4c959dbaac8bfc9a29
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345533"
---
# <a name="notification-of-stream-and-vertex-buffer-binding"></a>流和顶点缓冲区绑定通知


## <span id="ddk_notification_of_stream_vertex_buffer_binding_gg"></span><span id="DDK_NOTIFICATION_OF_STREAM_VERTEX_BUFFER_BINDING_GG"></span>


驱动程序通知的绑定到通过新的 DP2 令牌 D3DDP2OP 的特定流的顶点缓冲区\_SETSTREAMSOURCE，及其关联的 HAL 数据结构， [ **D3DHAL\_DP2SETSTREAMSOURCE**](https://msdn.microsoft.com/library/windows/hardware/ff545798).

 

 





