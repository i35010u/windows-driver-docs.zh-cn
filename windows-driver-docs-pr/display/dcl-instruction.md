---
title: DCL 指令格式
description: DCL 指令格式
ms.assetid: 2833fe6a-f430-4a34-936f-04e997063671
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ff5fd4c0c19bd26072167c252b4a9f1384a3dccd
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839768"
---
# <a name="dcl-instruction-format"></a>DCL 指令格式


## <span id="ddk_dcl_instruction_gg"></span><span id="DDK_DCL_INSTRUCTION_GG"></span>


DCL 指令声明寄存器。

### <a name="span-idformatspanspan-idformatspanformat"></a><span id="format"></span><span id="FORMAT"></span>形式

**象素着色器2仅\_0 和更高版本。**

**采样器状态仅寄存器。**

[指令标记](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[26:0\]** 保护. 设置为0x0。

**\[30:27\]** 设置为 D3DSAMPLER\_纹理\_类型（对于2D、多维数据集等）。

**\[31\]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示寄存器号和[寄存器类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)为 D3DSPR\_采样器。 这是此标记中使用的唯一字段。

**仅限输入或纹理寄存器。**

[指令标记](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[30:0\]** 保护. 设置为0x0。

**\[31\]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示输入或纹理寄存器号。 写入掩码字段指示已声明的组件。

**顶点着色器2仅\_0 和更高版本。**

**仅输入寄存器。**

[指令标记](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[4:0\]** D3DDECLUSAGE 值（即 D3DDECLUSAGE\_TEXCOORD、D3DDECLUSAGE\_NORMAL，等等）。

**\[15:5\]** 保护. 设置为0x0。

**\[19:16\]** 使用情况索引值。

**\[30:20\]** 保护. 设置为0x0。

**\[31\]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示寄存器号和[寄存器类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)为 D3DSPR\_输入。 写入掩码字段指示已声明的组件。

**象素着色器3仅\_0 和更高版本。**

**仅纹理寄存器。**

[指令标记](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[4:0\]** D3DDECLUSAGE 值（必须为 D3DDECLUSAGE\_TEXCOORD 或 D3DDECLUSAGE\_颜色）。

**\[15:5\]** 保护. 设置为0x0。

**\[19:16\]** 使用情况索引值。 对于 D3DDECLUSAGE\_TEXCOORD，必须为0-7。 对于 D3DDECLUSAGE\_颜色，必须为0。

**\[30:20\]** 保护. 设置为0x0。

**\[31\]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示寄存器号和[寄存器类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)为 D3DSPR\_纹理。 写入掩码字段指示已声明的组件。

**仅面部注册。**

[指令标记](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[30:0\]** 保护. 设置为0x0。

**\[31\]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示人脸登记簿。 写入掩码字段必须是完整的，但它是未使用的。 结果修饰符和转换比例字段必须为0（也未使用）。

**仅限位置寄存器。**

[指令标记](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[30:0\]** 保护. 设置为0x0。

**\[31\]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示位置寄存器。 写入掩码字段指示已声明的组件。

**顶点着色器 3\_0 和更高版本。**

**仅输出注册。**

[指令标记](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[4:0\]** D3DDECLUSAGE 值（即 D3DDECLUSAGE\_TEXCOORD、D3DDECLUSAGE\_NORMAL，等等）。

**\[15:5\]** 保护. 设置为0x0。

**\[19:16\]** 使用情况索引值。

**\[30:20\]** 保护. 设置为0x0。

**\[31\]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示寄存器号和[寄存器类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)为 D3DSPR\_输出。 写入掩码字段定义写入哪些组件。

请注意，用于描述输出的多个 DCL 说明可以使用相同的寄存器偏移量。 但是，每个 DCL 指令的写入掩码组件必须不同。 例如，以下在顶点着色器 3\_0 和更高版本中有效：

```registry
       DCL   o10.xy
       DCL   o10.zw
```

输出 DCL 指令必须声明由顶点着色器 3\_0 和更高版本写入的所有寄存器。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





