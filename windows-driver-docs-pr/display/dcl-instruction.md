---
title: DCL 指令格式
description: DCL 指令格式
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2bcaa1350e8ee6e779dc0609e1be5d0fae0f9639
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808463"
---
# <a name="dcl-instruction-format"></a>DCL 指令格式


## <span id="ddk_dcl_instruction_gg"></span><span id="DDK_DCL_INSTRUCTION_GG"></span>


DCL 指令声明寄存器。

### <a name="span-idformatspanspan-idformatspanformat"></a><span id="format"></span><span id="FORMAT"></span>形式

**仅限像素着色器 2 \_ 0 和更高版本。**

**采样器状态仅寄存器。**

[指令标记](instruction-token.md)

包含 D3DSIO \_ DCL。
DWORD 标记

具有以下位格式：

**\[ 26:0 \]** 已保留。 设置为0x0。

**\[ 30:27 \]** 设置为 \_ \_ 2d、cube 等的 D3DSAMPLER 纹理类型。

**\[ 31 \]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示寄存器号和 [寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type) 为 D3DSPR 采样器 \_ 。 这是此标记中使用的唯一字段。

**仅限输入或纹理寄存器。**

[指令标记](instruction-token.md)

包含 D3DSIO \_ DCL。
DWORD 标记

具有以下位格式：

**\[ 30:0 \]** 已保留。 设置为0x0。

**\[ 31 \]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示输入或纹理寄存器号。 写入掩码字段指示已声明的组件。

**顶点着色器 2 \_ 0 和更高版本。**

**仅输入寄存器。**

[指令标记](instruction-token.md)

包含 D3DSIO \_ DCL。
DWORD 标记

具有以下位格式：

**\[ 4:0 \]** D3DDECLUSAGE 值 (即 D3DDECLUSAGE \_ TEXCOORD、D3DDECLUSAGE \_ NORMAL 等) 。

**\[ 15:5 \]** 已保留。 设置为0x0。

**\[ 19:16 \]** 使用情况索引值。

**\[ 30:20 \]** 已保留。 设置为0x0。

**\[ 31 \]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示寄存器号和 [寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type) 为 D3DSPR \_ 输入。 写入掩码字段指示已声明的组件。

**仅限像素着色器 3 \_ 0 和更高版本。**

**仅纹理寄存器。**

[指令标记](instruction-token.md)

包含 D3DSIO \_ DCL。
DWORD 标记

具有以下位格式：

**\[ 4:0 \]** D3DDECLUSAGE 值 (必须是 D3DDECLUSAGE \_ TEXCOORD 或 D3DDECLUSAGE \_ COLOR) 。

**\[ 15:5 \]** 已保留。 设置为0x0。

**\[ 19:16 \]** 使用情况索引值。 对于 D3DDECLUSAGE \_ TEXCOORD，必须为0-7。 对于 D3DDECLUSAGE \_ 颜色，必须为0。

**\[ 30:20 \]** 已保留。 设置为0x0。

**\[ 31 \]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示寄存器号和 [寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type) 为 D3DSPR \_ 纹理。 写入掩码字段指示已声明的组件。

**仅面部注册。**

[指令标记](instruction-token.md)

包含 D3DSIO \_ DCL。
DWORD 标记

具有以下位格式：

**\[ 30:0 \]** 已保留。 设置为0x0。

**\[ 31 \]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示人脸登记簿。 写入掩码字段必须是完整的，但它是未使用的。 结果-修饰符和移位刻度字段必须是 0 (也不) 使用。

**仅限位置寄存器。**

[指令标记](instruction-token.md)

包含 D3DSIO \_ DCL。
DWORD 标记

具有以下位格式：

**\[ 30:0 \]** 已保留。 设置为0x0。

**\[ 31 \]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示位置寄存器。 写入掩码字段指示已声明的组件。

**顶点着色器 3 \_ 0 和更高版本。**

**仅输出注册。**

[指令标记](instruction-token.md)

包含 D3DSIO \_ DCL。
DWORD 标记

具有以下位格式：

**\[ 4:0 \]** D3DDECLUSAGE 值 (即 D3DDECLUSAGE \_ TEXCOORD、D3DDECLUSAGE \_ NORMAL 等) 。

**\[ 15:5 \]** 已保留。 设置为0x0。

**\[ 19:16 \]** 使用情况索引值。

**\[ 30:20 \]** 已保留。 设置为0x0。

**\[ 31 \]** 设置为0x1。

[目标参数标记](destination-parameter-token.md)

指示寄存器号和 [寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type) 为 D3DSPR \_ 输出。 写入掩码字段定义写入哪些组件。

请注意，用于描述输出的多个 DCL 说明可以使用相同的寄存器偏移量。 但是，每个 DCL 指令的写入掩码组件必须不同。 例如，下面的在顶点着色器 3 \_ 0 和更高版本中有效：

```registry
       DCL   o10.xy
       DCL   o10.zw
```

输出 DCL 指令必须声明由顶点着色器 3 \_ 0 和更高版本写入的所有寄存器。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

