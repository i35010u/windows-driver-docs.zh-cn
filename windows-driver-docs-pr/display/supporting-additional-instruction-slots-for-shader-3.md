---
title: 支持着色器 3 的其他指令槽
description: 支持着色器 3 的其他指令槽
ms.assetid: 8ff00178-cd08-42ce-8dea-127fc0d04733
keywords:
- 指令槽 WDK DirectX 9.0
- 着色器 WDK DirectX 9.0
- 像素着色器 WDK DirectX 9.0
- 顶点着色器 WDK DirectX 9.0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1859e6504b6f9eb7664d74864a3a453750efe2f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375905"
---
# <a name="supporting-additional-instruction-slots-for-shader-3"></a>支持着色器 3 的其他指令槽


## <span id="ddk_supporting_additional_instruction_slots_for_shader_3_gg"></span><span id="DDK_SUPPORTING_ADDITIONAL_INSTRUCTION_SLOTS_FOR_SHADER_3_GG"></span>


对任一着色器类型的支持像素或顶点着色器版本 3.0 及更高版本的显示设备必须支持至少 512 指令槽。 但是，此显示设备可以支持任一着色器类型最多 32768 指令槽。

若要指示设备支持的指令槽的顶点着色器 3.0、 设备集的 DirectX 9.0 驱动程序的最大数目**MaxVertexShader30InstructionSlots**到 D3DCAPS9 结构中的成员最大数目。

若要指示设备支持的指令槽的像素着色器 3.0、 设备集的 DirectX 9.0 驱动程序的最大数目**MaxPixelShader30InstructionSlots** D3DCAPS9 结构为最大值中的成员数。

DirectX 9.0 驱动程序的最大数的指令槽像素和顶点 3.0 着色器可能会不同，因为可以设置**MaxVertexShader30InstructionSlots**和**MaxPixelShader30InstructionSlots**为不同的值。 该驱动程序可以从 512 设置指令槽的最大数目为 32768。 如果该驱动程序设置**MaxVertexShader30InstructionSlots**或**MaxPixelShader30InstructionSlots**允许范围之外的值，该驱动程序将无法加载。

该驱动程序在响应中返回 D3DCAPS9 结构**GetDriverInfo2**查询类似于如何返回 D3DCAPS8 结构，如中所述[报告 DirectX 8.0 样式 Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)。 此查询的支持中所述[支持 GetDriverInfo2](supporting-getdriverinfo2.md)。

 

 





