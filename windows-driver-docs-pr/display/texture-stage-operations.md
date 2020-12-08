---
title: 纹理阶段操作
description: 纹理阶段操作
keywords:
- 多纹理 WDK Direct3D，纹理阶段
- 纹理阶段 WDK Direct3D
- 纹理管理 WDK Direct3D，阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 074660cd54bcfa98da226a4446241fdb352e9d73
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838937"
---
# <a name="texture-stage-operations"></a>纹理阶段操作


## <span id="ddk_texture_stage_operations_gg"></span><span id="DDK_TEXTURE_STAGE_OPERATIONS_GG"></span>


应用程序通过调用 **IDirect3DDevice7：： SetTextureStageState** 方法为纹理阶段执行混合操作。 多个纹理混合操作由一组纹理混合单元阶段执行。 每个可单独进行编程以执行各种纹理混合操作，这些操作由参数选择。 有关 **IDirect3DDevice7：： SetTextureStageState** 的说明，请参阅 Direct3D SDK 文档。

Direct3D 不提供一种机制来指定每个混合阶段引入的纹理。 饱和度定义为在管道中的纹理阶段之间发生，但在每个阶段中应尽可能晚地发生。

在 D3DTEXTUREOP 中枚举的下列操作是 PC98 兼容性符合性所必需的：

-   \_禁用 D3DTOP

-   D3DTOP \_ SELECTARG1，D3DTOP \_ SELECTARG2

-   D3DTOP \_ 伯

-   D3DTOP \_ 添加

-   D3DTOP \_ BLENDTEXTUREALPHA

\_对于阶段 one，默认值为 D3DTOP 伯，D3DTOP \_ 禁用所有其他阶段。 D3DTOP \_ 伯用于向后兼容阶段，但默认情况下，应禁用所有纹理。

 

 





