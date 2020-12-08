---
title: D3dCreateSurfaceEx 和后备图面
description: D3dCreateSurfaceEx 和后备图面
keywords:
- 上下文 WDK Direct3D，D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- 支持面 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc0098c42884bc44ecf124b83a08d678670b58ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838505"
---
# <a name="d3dcreatesurfaceex-and-backing-surfaces"></a>D3dCreateSurfaceEx 和后备图面


## <span id="ddk_d3dcreatesurfaceex_and_backing_surfaces_gg"></span><span id="DDK_D3DCREATESURFACEEX_AND_BACKING_SURFACES_GG"></span>


[**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 也可用于作为托管图面的系统内存持久副本的 *后备面*。 这样，驱动程序便可为表面分配驱动程序端结构，并对 \_ 系统到视频纹理下载的 D3DDP2OP TEXBLT 标记做出响应。

[**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 应永远不会基于所请求的后备 surface 的格式和功能失败，因为模拟代码可以支持和处理图面。 但是，其他失败条件是有效的。 例如，如果驱动程序维护专用数据结构并且内存空间不足，驱动程序可能会 **D3dCreateSurfaceEx** 。

对于不支持像素格式的后备 surface 格式，驱动程序不应 [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 。 可以创建此类面，以便与软件光栅程序结合使用。 驱动程序只应忽略它不支持的支持面。  (或者，驱动程序可以创建驱动程序端结构，但不会随后将相应的句柄发送到驱动程序。 ) 

对于这些后备面， [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 会导致错误代码传播到应用程序;然后，驱动程序可能会在仅模拟模式下影响应用程序。 驱动程序对此类情况的响应可以通过运行位于 DirectX 7.0 SDK 上的 *ddtest.exe* 应用程序进行测试。 运行 *ddtest.exe* ，尝试创建驱动程序不支持的格式的后备 surface 纹理，但 directdraw 仿真层支持 (这些格式的列表，可在 directdraw SDK 文档) 中找到。

 

