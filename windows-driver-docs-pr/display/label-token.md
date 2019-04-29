---
title: 标签标记
description: 标签标记
ms.assetid: 29b2b4b1-c599-4bea-9d83-3a10eedac4a6
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: bae11eb53c3de8110e1068cc9c5bcac5e95be8f6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363091"
---
# <a name="label-token"></a>标签标记


## <span id="ddk_label_token_gg"></span><span id="DDK_LABEL_TOKEN_GG"></span>


标签标记仅用于某些操作 (例如，D3DSIO\_CALLNZ) 并由以下位组成：

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>Bits

<span id="_10_00_"></span>**\[10:00\]** 位 0 到 10 指示寄存器号 （注册文件中的偏移量）。

<span id="_12_11_"></span>**\[12:11\]**  bits 11 和 12 是第四个和第五个 bits \[3，4\]用于指示[注册类型](https://msdn.microsoft.com/library/windows/hardware/ff569707)。

<span id="_27_13_"></span>**\[27:13\]** 保留的像素着色器 (PS) 和顶点着色器 (VS) 的所有版本。 此值设置为 0x0。

<span id="_30_28_"></span>**\[30:28\]** 到 30 位 28 个为前三个位\[0,1,2\]用于指示[注册类型](https://msdn.microsoft.com/library/windows/hardware/ff569707)。

<span id="_31_"></span>**\[31\]** 位 31 为 0x1。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

标签标记的格式是相同[源参数标记](source-parameter-token.md)只不过仅注册数量和类型使用该字段。

28、 29、 30、 11 和 12 位窗体为 5 位值，该值指示注册类型。 有关注册类型的信息，请参阅[着色器注册类型](https://msdn.microsoft.com/library/windows/hardware/ff569707)。 标签标记的注册类型必须指定为 D3DSPR\_标签。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





