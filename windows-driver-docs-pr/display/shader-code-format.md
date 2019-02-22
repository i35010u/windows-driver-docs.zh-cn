---
title: 着色器代码格式
description: 着色器代码格式
ms.assetid: 62377d19-8e45-4d0c-b974-0c0417d1a948
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 506c7be066efb38ef8ef473c6194ad1dd1c5e27a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543856"
---
# <a name="shader-code-format"></a>着色器代码格式


## <span id="ddk_shader_code_format_gg"></span><span id="DDK_SHADER_CODE_FORMAT_GG"></span>


若要创建像素或顶点着色器的命令组成的着色器代码组。 这些代码指示如何创建着色器上的驱动程序。 每个着色器代码中的令牌的格式确定其唯一性。 一个[着色器代码令牌](shader-code-tokens.md)为具有特定格式 dword 值。

DirectX3D 运行时的代码传递到驱动程序之前会验证着色器代码。 当驱动程序在到达着色器代码时，该驱动程序可以解释代码，因为代码的格式有效。 驱动程序读取着色器代码的令牌，该代码的解释。

每个单独的着色器代码将使用常规的令牌布局格式。 第一个标记必须是[版本标记](version-token.md)。 版本标记提供了代码的版本号，并且还确定代码是否为像素或顶点着色器。 着色器内容遵循版本标记，且由各种[指令令牌](instruction-token.md)，与可能是混合[注释标记](comment-token.md)和空白区域。 根据指定的指令令牌的精确操作[标签](label-token.md)， [destination 参数](destination-parameter-token.md)，并[源参数标记](source-parameter-token.md)也可以是一部分的着色器内容，并按照指令令牌。 例如，如果指定的指令令牌[ADD 指令](https://msdn.microsoft.com/library/windows/hardware/ff538212)，该驱动程序确定一个目标和两个源参数标记遵循指令令牌。 [结束令牌](end-token.md)完成的着色器代码。

安装说明进行操作 (例如，D3DSIO\_DCL 和 D3DSIO\_DEF) 包含格式独一无二的标记。

每个着色器指令包含特定的令牌格式。 [着色器操作代码](https://msdn.microsoft.com/library/windows/hardware/ff569706)部分介绍了每个着色器指令的令牌格式。

着色器说明与主指令开头和结尾 D3DSIO\_RET 或 D3DSIO\_结束指令。 子例程按照 D3DSIO\_RET 指令。

有关可以在指令的令牌中指定的操作的详细信息的最新的 DirectX SDK 文档中，请参阅像素着色器引用和顶点着色器引用。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





