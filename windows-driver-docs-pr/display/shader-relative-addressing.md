---
title: 着色器相对寻址
description: 着色器相对寻址
ms.assetid: 7f936b56-cd41-4df5-8fc0-b8a7332ca7fa
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 95b5df1eb45f01a58777b0e691d699c04d0fbede
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577067"
---
# <a name="shader-relative-addressing"></a>着色器相对寻址


## <span id="ddk_shader_relative_addressing_gg"></span><span id="DDK_SHADER_RELATIVE_ADDRESSING_GG"></span>


中的位 13 使用像素和顶点着色器版本支持相对地址可以指定该相对寻址[目标](destination-parameter-token.md)并[源参数标记](source-parameter-token.md)。 当指定相对地址时，其他的 DWORD 标记遵循目标或源参数标记。

请注意，此相对寻址令牌是只提供给顶点着色器版本 2\_0 和更高版本和像素着色器版本 3 的\_0 和更高版本。 相对地址不用于像素着色器的版本早于 3\_0。

此相对寻址令牌格式与目标相同或源参数标记和以下规则适用：

-   仅 D3DSPR\_ADDR 或 D3DSPR\_循环可用作[注册类型](https://msdn.microsoft.com/library/windows/hardware/ff569707)。

-   源参数标记中的 swizzle 位用于确定注册组件。

-   第 31 位为 0x1。

-   使用注册偏移量。

-   不使用的所有其他位。

地址寄存器和 aL 注册用于常量寄存器的相对地址。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





