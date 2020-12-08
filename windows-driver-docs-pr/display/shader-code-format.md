---
title: 着色器代码格式
description: 着色器代码格式
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: bbbe4bc0849131d0d8bcb7654c05b7f2971d4f50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817781"
---
# <a name="shader-code-format"></a>着色器代码格式


## <span id="ddk_shader_code_format_gg"></span><span id="DDK_SHADER_CODE_FORMAT_GG"></span>


用于创建像素或顶点着色器的命令由一组着色器代码组成。 这些代码指示驱动程序如何创建着色器。 每个着色器代码内的标记格式确定其唯一性。 [着色器代码令牌](shader-code-tokens.md)是具有特定格式的 DWORD。

在将代码传递到驱动程序之前，DirectX3D 运行时将验证着色器代码。 当着色器代码到达驱动程序时，驱动程序可以解释代码，因为代码的格式有效。 驱动程序读取着色器代码的标记以解释代码。

每个单独的着色器代码均使用常规令牌布局进行格式设置。 第一个标记必须是 [版本标记](version-token.md)。 版本标记提供代码的版本号，还确定代码是用于像素着色器还是用于顶点着色器。 着色器内容遵循版本标记，由各种 [指令标记](instruction-token.md)组成，可能与 [注释标记](comment-token.md) 和空格混合。 根据指令令牌指定的精确操作， [标签](label-token.md)、 [目标参数](destination-parameter-token.md)和 [源参数令牌](source-parameter-token.md) 也可以是着色器内容的一部分，并遵循指令标记。 例如，如果指令令牌指定 [ADD 指令](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type)，则驱动程序将确定一个目标和两个源参数标记跟在指令标记之后。 [结束标记](end-token.md)完成着色器代码。

设置说明 (例如，D3DSIO \_ DCL 和 D3DSIO \_ DEF) 包含唯一格式的令牌。

每个着色器指令都包含特定的令牌格式。 [着色器操作代码](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type)部分描述每个着色器指令的令牌格式。

着色器说明从主指令开始，以 D3DSIO \_ RET 或 D3DSIO \_ 结束指令结束。 子例程遵循 D3DSIO \_ RET 指令。

有关可在指令标记中指定的操作的详细信息，请参阅最新的 DirectX SDK 文档中的 "像素着色器参考" 和 "顶点着色器参考"。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

