---
title: 销毁与 Direct3D 上下文关联的对象
description: 销毁与 Direct3D 上下文关联的对象
ms.assetid: b464eb31-6062-4c0c-90a2-2de39b5a85ac
keywords:
- 内存泄漏 WDK DirectX 9。0
- 上下文 WDK Direct3D、DirectX 9。0
- 销毁与上下文 WDK DirectX 9.0 相关的对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c82680b1f191d5255aeda5b1236ea6508404312
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065914"
---
# <a name="destroying-objects-associated-with-a-direct3d-context"></a>销毁与 Direct3D 上下文关联的对象


## <span id="ddk_destroying_objects_associated_with_a_direct3d_context_gg"></span><span id="DDK_DESTROYING_OBJECTS_ASSOCIATED_WITH_A_DIRECT3D_CONTEXT_GG"></span>


本主题适用于 DirectX 7.0 和更高版本。

若要防止内存泄漏，在调用驱动程序的 [**D3dContextDestroy**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextdestroycb) 函数时，显示驱动程序必须释放与 Direct3D 上下文相关联的所有对象。 例如，这些对象包括顶点着色 [器、顶点](direct3d-shaders.md)着色器的 [声明和代码](separating-declarations-and-code-for-vertex-shaders.md)、用于 [异步查询](supporting-asynchronous-query-operations.md)的资源，以及纹理资源。

 

