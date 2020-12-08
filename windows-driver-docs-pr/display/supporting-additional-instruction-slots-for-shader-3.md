---
title: 支持着色器 3 的其他指令槽
description: 支持着色器 3 的其他指令槽
keywords:
- 指令槽 WDK DirectX 9。0
- 着色器 WDK DirectX 9。0
- 象素着色器 WDK DirectX 9。0
- 顶点着色器 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8df753a3fcebb64415a4c3221bd86a5bc0c05082
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830061"
---
# <a name="supporting-additional-instruction-slots-for-shader-3"></a>支持着色器 3 的其他指令槽


## <span id="ddk_supporting_additional_instruction_slots_for_shader_3_gg"></span><span id="DDK_SUPPORTING_ADDITIONAL_INSTRUCTION_SLOTS_FOR_SHADER_3_GG"></span>


支持像素或顶点着色器版本3.0 及更高版本的显示设备必须支持至少512个着色器类型的指令槽。 但是，此显示设备最多可支持32768个着色器类型的指令槽。

为指示设备支持的顶点着色器3.0 的最大指令槽数，设备的 DirectX 9.0 驱动程序将 D3DCAPS9 结构的 **MaxVertexShader30InstructionSlots** 成员设置为最大数目。

若要指示设备支持的像素着色器3.0 的指令槽的最大数量，设备的 DirectX 9.0 驱动程序将 D3DCAPS9 结构的 **MaxPixelShader30InstructionSlots** 成员设置为最大数目。

由于像素和顶点3.0 着色器的最大指令槽数可能不同，因此 DirectX 9.0 驱动程序可以将 **MaxVertexShader30InstructionSlots** 和 **MaxPixelShader30InstructionSlots** 设置为不同的值。 驱动程序可以将指令槽的最大数目设置为512到32768。 如果驱动程序将 **MaxVertexShader30InstructionSlots** 或 **MaxPixelShader30InstructionSlots** 设置为允许范围之外的值，则无法加载该驱动程序。

驱动程序将返回 D3DCAPS9 结构，以响应 **GetDriverInfo2** 查询，如 [报告 DirectX 8.0 Style Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述的那样返回 D3DCAPS8 结构。 支持 [GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此查询的支持。

 

 





