---
title: 标签标记
description: 标签标记
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 96289b2f1485d18d5b7e8376d1b0303d04e61c69
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792977"
---
# <a name="label-token"></a>标签标记


## <span id="ddk_label_token_gg"></span><span id="DDK_LABEL_TOKEN_GG"></span>


标签令牌仅用于某些操作 (例如 D3DSIO \_ CALLNZ) ，由以下位构成：

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>带宽

<span id="_10_00_"></span>**\[ 10:00 \]** 位0到10表示寄存器号)  (偏移量。

<span id="_12_11_"></span>**\[ 12:11 \]** 位11和12是 \[ \] 用于指示 [寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)的第四个和第五个第三位。

<span id="_27_13_"></span>**\[ 27:13 \]** 为像素着色器 (PS) 和顶点着色器 (与) 一起预留。 此值设置为0x0。

<span id="_30_28_"></span>**\[ 30:28 \]** 位28到30是 \[ \] 用于指示 [寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)的前三位0、1、2。

<span id="_31_"></span>**\[ 31 \]** 位31为0x1。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

标签标记的格式与 [源参数标记](source-parameter-token.md) 相同，不同之处在于只使用寄存器号和类型字段。

位28、29、30、11和12构成一个指示寄存器类型的5位值。 有关寄存器类型的信息，请参阅 [着色器寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)。 标签标记的寄存器类型必须指定为 D3DSPR \_ 标签。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

