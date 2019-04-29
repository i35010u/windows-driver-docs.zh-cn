---
title: 纹理阶段操作
description: 纹理阶段操作
ms.assetid: da2213bb-41f1-440b-8f69-19f69e739954
keywords:
- 多个纹理 WDK Direct3D，纹理阶段
- 纹理阶段 WDK Direct3D
- 纹理管理 WDK Direct3D，阶段
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7020feff0a5f9706d4d7e2229f6f77ac95693321
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362708"
---
# <a name="texture-stage-operations"></a>纹理阶段操作


## <span id="ddk_texture_stage_operations_gg"></span><span id="DDK_TEXTURE_STAGE_OPERATIONS_GG"></span>


应用程序通过调用执行混合操作纹理阶段**IDirect3DDevice7::SetTextureStageState**方法。 由一组的纹理值混合处理单元阶段执行的多个纹理混合操作。 其中每项功能可以分别通过编程来执行各种操作，由一个参数选择值混合处理的纹理。 有关的说明**IDirect3DDevice7::SetTextureStageState**，请参阅 Direct3D SDK 文档。

Direct3D 不提供一种机制，用于指定在每个混合阶段引入了多个纹理。 饱和度定义在管道中，纹理阶段之间发生，但它应尽可能晚发生在每个阶段。

中 D3DTEXTUREOP 枚举的以下操作所需 PC98 兼容性法规遵从性：

-   D3DTOP\_禁用

-   D3DTOP\_SELECTARG1、 D3DTOP\_SELECTARG2

-   D3DTOP\_MODULATE

-   D3DTOP\_添加

-   D3DTOP\_BLENDTEXTUREALPHA

默认值为 D3DTOP\_MODULATE 第一，阶段和 D3DTOP\_禁用对于所有其他阶段。 D3DTOP\_MODULATE 用于向后兼容，第一阶段，但默认情况下，应禁用所有纹理。

 

 





