---
title: 创建和销毁上下文
description: 创建和销毁上下文
ms.assetid: 31462b0a-ed06-4138-ab91-7ec98bc5ff14
keywords:
- 上下文 WDK Direct3D，创建
- 上下文 WDK Direct3D，销毁
- D3dContextCreate
- D3dContextDestroy
- 销毁上下文 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 324ec4e0079ac28e2ae9442976096b0dfefe0627
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715352"
---
# <a name="creating-and-destroying-a-context"></a>创建和销毁上下文


## <span id="ddk_creating_and_destroying_a_context_gg"></span><span id="DDK_CREATING_AND_DESTROYING_A_CONTEXT_GG"></span>


驱动程序必须创建和初始化设备特定的上下文，该上下文封装了执行呈现所需的状态信息。 状态不在上下文之间共享;因此，驱动程序必须为其创建的每个上下文维护完整的状态信息。

若要创建上下文，驱动程序应执行以下操作：

-   分配设备特定的上下文，并将其初始化为零。

-   请参阅 [**D3dContextCreate**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb) ，了解该回调中要执行的其他步骤。 当应用程序创建 Direct3D HAL 设备时，将调用 **D3dContextCreate** 回调。 驱动程序必须实现此回调。

驱动程序必须能够在创建的上下文中引用 [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 创建的所有纹理句柄。 这使得驱动程序可以在对 [**D3dContextDestroy**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb) 函数进行调用时，清理与在此上下文中创建的纹理相关的所有驱动程序特定数据。

当应用程序请求某个 Direct3D HAL 设备被销毁时，Direct3D 会调用 [**D3dContextDestroy**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb) 。 驱动程序应释放分配给指定上下文的所有资源。 例如，这些资源包括纹理资源、顶点和像素 [着色](direct3d-shaders.md)器、 [用于顶点着色的声明和代码](separating-declarations-and-code-for-vertex-shaders.md)以及用于 [异步查询](supporting-asynchronous-query-operations.md)的资源。

 

