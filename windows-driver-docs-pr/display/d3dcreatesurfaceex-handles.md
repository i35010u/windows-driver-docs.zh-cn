---
title: D3dCreateSurfaceEx 句柄
description: D3dCreateSurfaceEx 句柄
ms.assetid: ada78f89-422b-470d-9423-09968ae113e8
keywords:
- 上下文 WDK Direct3D，D3dCreateSurfaceEx
- D3dCreateSurfaceEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bca612a06401c55fb85c3df817227d55600ae1c0
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715476"
---
# <a name="d3dcreatesurfaceex-handles"></a>D3dCreateSurfaceEx 句柄


## <span id="ddk_d3dcreatesurfaceex_handles_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_GG"></span>


某些情况下可能会导致对无效、损坏的图面调用 [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 。 驱动程序可以轻松地处理这种情况，只需忽略 **)  (** [**DD \_ 表面 \_ 全局**](/windows/win32/api/ddrawint/ns-ddrawint-_dd_surface_global)结构的成员为零的视频内存图面的任何**D3dCreateSurfaceEx**调用。 但是，驱动程序可以获取 **D3dCreateSurfaceEx** 调用，其系统内存表面的 **fpVidMem** 值为零，这意味着系统内存图面正在销毁。 然后，该驱动程序应释放与此表面相关的任何现有驱动程序端数据。

 

