---
title: D3dCreateSurfaceEx 句柄
description: D3dCreateSurfaceEx 句柄
ms.assetid: ada78f89-422b-470d-9423-09968ae113e8
keywords:
- 上下文 WDK Direct3D D3dCreateSurfaceEx
- D3dCreateSurfaceEx
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0232b99cce828c8f7f0e863e79ee3a52da21352
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370153"
---
# <a name="d3dcreatesurfaceex-handles"></a>D3dCreateSurfaceEx 句柄


## <span id="ddk_d3dcreatesurfaceex_handles_gg"></span><span id="DDK_D3DCREATESURFACEEX_HANDLES_GG"></span>


某些情况下可能会导致[ **D3dCreateSurfaceEx** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)要调用的是无效、 销毁的表面。 驱动程序可以通过只需忽略任何能够稳定地处理这种情况下**D3dCreateSurfaceEx**调用具有视频内存面的**fpVidMem** (隶属[ **DD\_面\_GLOBAL** ](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_surface_global)结构) 的零。 但是，可以获取驱动程序**D3dCreateSurfaceEx**调用与具有系统内存面**fpVidMem**值为零，这意味着系统内存图面是处于销毁过程中。 该驱动程序随后应释放与此问题相关的任何现有端驱动程序的数据。

 

 





