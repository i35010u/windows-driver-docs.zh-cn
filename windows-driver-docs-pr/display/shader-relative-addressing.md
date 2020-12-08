---
title: 着色器相对寻址
description: 着色器相对寻址
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 22805ae3e71eca2c07786dc7f4f9b3db764df394
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825697"
---
# <a name="shader-relative-addressing"></a>着色器相对寻址

支持相对寻址的像素和顶点着色器版本可指定在 [目标](destination-parameter-token.md) 和 [源参数令牌](source-parameter-token.md)的第13位中使用相对寻址。 如果指定了相对寻址，则目标或源参数标记后面会出现一个额外的 DWORD 标记。

请注意，此相对寻址标记仅适用于顶点着色器版本 2 \_ 0 和更高版本以及像素着色器版本 3 \_ 0 及更高版本。 相对寻址不用于低于 3 0 的像素着色器版本 \_ 。

此相对地址标记的格式与目标或源参数标记的格式相同，以下规则适用：

-   只有 D3DSPR \_ 地址或 D3DSPR \_ 循环才能用作 [寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)。

-   使用源参数令牌中的 Swizzle 位来确定注册组件。

-   位31为0x1。

-   使用寄存器偏移量。

-   不使用所有其他位。

地址寄存器和 aL 寄存器用于固定寄存器的相对寻址。

## <a name="requirements"></a>要求

在 Windows Vista 和更高版本的 Windows 操作系统中可用。
