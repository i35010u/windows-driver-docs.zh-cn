---
title: D3dCreateSurfaceEx 和后备图面
description: D3dCreateSurfaceEx 和后备图面
ms.assetid: aad37654-616f-4cbd-9a9c-07458fb61947
keywords:
- 上下文 WDK Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
- 备份 WDK Direct3D 图面
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0e24557d2aeeca83c093b38e2b6d8b1bbde6b275
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370164"
---
# <a name="d3dcreatesurfaceex-and-backing-surfaces"></a>D3dCreateSurfaceEx 和后备图面


## <span id="ddk_d3dcreatesurfaceex_and_backing_surfaces_gg"></span><span id="DDK_D3DCREATESURFACEEX_AND_BACKING_SURFACES_GG"></span>


[**D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)也称为用于*备份图面*，这是托管应用层的永久副本的系统内存。 这将允许驱动程序分配面端驱动程序的结构并响应 D3DDP2OP\_TEXBLT 令牌系统进行视频纹理下载。

[**D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)永远不应基于的格式和功能请求，因为仿真代码无法支持和处理表面的后备图面上的故障。 但是，失败的其他条件依然有效。 例如，驱动程序可能会失败**D3dCreateSurfaceEx**如果维护专用的数据结构，并且内存空间不足。

该驱动程序不会将故障[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)备份图面上，它不支持的像素格式的格式。 可能以软件光栅器用于创建此类表面。 驱动程序只是应忽略它不支持的后备图面。 （或者，驱动程序可以创建端驱动程序的结构，但相应的句柄随后从未发送到该驱动程序。）

对于这些后备图面中， [ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)原因失败代码传播到应用程序; 该驱动程序然后可能会影响仅限仿真模式中的应用程序。 可以通过运行测试这种情况下的驱动程序的响应*ddtest.exe*位于 DirectX 7.0 SDK 的应用程序。 运行*ddtest.exe* ，然后尝试创建后备图面上纹理的格式不受支持的驱动程序，但 （DirectDraw SDK 文档中可以找到这些格式的列表） 的 DirectDraw 仿真层支持。

 

 





