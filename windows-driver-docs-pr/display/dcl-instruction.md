---
title: DCL 指令格式
description: DCL 指令格式
ms.assetid: 2833fe6a-f430-4a34-936f-04e997063671
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0117a883bd9ac1a8bd1090b368768fdfa1d56ff4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358672"
---
# <a name="dcl-instruction-format"></a>DCL 指令格式


## <span id="ddk_dcl_instruction_gg"></span><span id="DDK_DCL_INSTRUCTION_GG"></span>


DCL 指令声明寄存器。

### <a name="span-idformatspanspan-idformatspanformat"></a><span id="format"></span><span id="FORMAT"></span>格式

**像素着色器 2\_0 及更高版本。**

**采样器状态仅注册。**

[指令令牌](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[26:0\]** 保留。 设为 0x0。

**\[30:27\]** 设置为 D3DSAMPLER\_纹理\_类型 2D、 多维数据集，等等。

**\[31\]** 设置为 0x1。

[目标参数标记](destination-parameter-token.md)

指示寄存器号与[注册类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3dshader_param_register_type)作为 D3DSPR\_采样器。 这些是使用此令牌中的唯一字段。

**输入或纹理仅注册。**

[指令令牌](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[30:0\]** 保留。 设为 0x0。

**\[31\]** 设置为 0x1。

[目标参数标记](destination-parameter-token.md)

指示输入或纹理寄存器号。 写掩码字段指示声明的组件。

**顶点着色器 2\_0 及更高版本。**

**输入的注册。**

[指令令牌](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[4:0\]**  D3DDECLUSAGE 值 (即，D3DDECLUSAGE\_TEXCOORD、 D3DDECLUSAGE\_正常，等等)。

**\[15:5\]** 保留。 设为 0x0。

**\[19:16\]** 使用索引值。

**\[30:20\]** 保留。 设为 0x0。

**\[31\]** 设置为 0x1。

[目标参数标记](destination-parameter-token.md)

指示寄存器号与[注册类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3dshader_param_register_type)作为 D3DSPR\_输入。 写掩码字段指示声明的组件。

**像素着色器 3\_0 及更高版本。**

**纹理寄存器。**

[指令令牌](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[4:0\]**  D3DDECLUSAGE 值 (必须是 D3DDECLUSAGE\_TEXCOORD 或 D3DDECLUSAGE\_颜色)。

**\[15:5\]** 保留。 设为 0x0。

**\[19:16\]** 使用索引值。 有关 D3DDECLUSAGE\_TEXCOORD，必须是 0 到 7。 有关 D3DDECLUSAGE\_颜色，必须为 0。

**\[30:20\]** 保留。 设为 0x0。

**\[31\]** 设置为 0x1。

[目标参数标记](destination-parameter-token.md)

指示寄存器号与[注册类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3dshader_param_register_type)作为 D3DSPR\_纹理。 写掩码字段指示声明的组件。

**仅注册人脸。**

[指令令牌](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[30:0\]** 保留。 设为 0x0。

**\[31\]** 设置为 0x1。

[目标参数标记](destination-parameter-token.md)

指示人脸注册。 写掩码字段必须完整，尽管它是未使用。 结果修改键和 shift 规模字段必须为 0 （还未使用）。

**仅限于位置注册。**

[指令令牌](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[30:0\]** 保留。 设为 0x0。

**\[31\]** 设置为 0x1。

[目标参数标记](destination-parameter-token.md)

指示位置注册。 写掩码字段指示声明的组件。

**顶点着色器 3\_0 及更高版本。**

**仅注册输出。**

[指令令牌](instruction-token.md)

包含 D3DSIO\_DCL。
DWORD 标记

具有以下位格式：

**\[4:0\]**  D3DDECLUSAGE 值 (即，D3DDECLUSAGE\_TEXCOORD、 D3DDECLUSAGE\_正常，等等)。

**\[15:5\]** 保留。 设为 0x0。

**\[19:16\]** 使用索引值。

**\[30:20\]** 保留。 设为 0x0。

**\[31\]** 设置为 0x1。

[目标参数标记](destination-parameter-token.md)

指示寄存器号与[注册类型](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/d3d9types/ne-d3d9types-_d3dshader_param_register_type)作为 D3DSPR\_输出。 写掩码字段定义哪个组件编写。

请注意几个 DCL 说明信息，其中描述了输出，可以使用相同的注册偏移量。 但是，每个 DCL 指令的写掩码组件必须不同。 例如，以下是在顶点着色器 3 中有效\_0 和更高版本：

```registry
       DCL   o10.xy
       DCL   o10.zw
```

输出 DCL 指令必须声明编写的顶点着色器 3 的所有寄存器\_0 和更高版本。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





