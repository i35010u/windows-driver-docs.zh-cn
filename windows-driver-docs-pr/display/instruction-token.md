---
title: 指令标记
description: 指令标记
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: b66d73a29ce60f2014ab5df209f00184d1388d4c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792329"
---
# <a name="instruction-token"></a>指令标记


## <span id="ddk_instruction_token_gg"></span><span id="DDK_INSTRUCTION_TOKEN_GG"></span>


指令标记告知特定操作的驱动程序执行，由以下位构成：

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>带宽

<span id="_15_00_"></span>**\[ 15:00 \]** 位0到15指示 [操作代码](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type)。 D3DSIO \_ \* 是操作代码的一个示例，其中 \* 表示指令。 例如，下面的代码段显示了一个 [ADD 指令](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type)：

```cpp
// D3DSIO_ADD d, s1, s2
```

<span id="_23_16_"></span>**\[ 23:16 \]** 位16到23表示与操作代码相关的特定控件。

<span id="_27_24_"></span>**\[ 27:24 \]** 对于低于 2 0 的像素和顶点着色器版本 \_ ，将保留位24到27，并将其设置为0x0。

对于像素和顶点着色器版本 2 \_ 0 和更高版本，0到27位指定指令标记本身之外的指令的大小（以 dword 表示，其中包含指令标记) 之外的指令的标记数） (。

<span id="_28_"></span>如果像素和顶点着色器版本低于 2 0，则保留 **第 28 \[ 位并将其设置为0x0。 \]** \_

对于像素和顶点着色器版本 2 \_ 0 和更高版本，第28位指示指令是否为依据 (也就是说，在着色器代码末尾包含一个额外的谓词源标记。 如果此位设置为0x1，则指令为依据。

<span id="_29_"></span>**\[ 29 \]** 个保留的。 此值设置为0x0。

<span id="_30_"></span>**\[ 30 \]** 对于低于 2 0 的像素着色器版本 \_ ，位30是共同颁发位。 如果设置为1，则按前面的说明执行此指令;否则，单独执行。

对于像素着色器版本 2 \_ 0 和更高版本以及所有顶点着色器版本，保留位30，并将其设置为0x0。

<span id="_31_"></span>**\[ 31 \]** 位31为零 (0x0) 。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

请参阅最新的 DirectX SDK 文档中的 "像素着色器参考" 和 "顶点着色器参考"，详细了解可以在0到15位指令标记中指定的操作。

在 DirectX3D 运行时从应用程序接收着色器代码后，运行时将验证代码，然后将代码传递给驱动程序。 通常情况下，运行时为汇编程序说明提供 "D3DSIO \_ " 来创建操作代码。 例如，以下汇编说明与内核模式操作相对应：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">汇编程序指令</th>
<th align="left">内核模式操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>add</strong></p></td>
<td align="left"><p>D3DSIO_ADD</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>mov</strong></p></td>
<td align="left"><p>D3DSIO_MOV</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>sub</strong></p></td>
<td align="left"><p>D3DSIO_SUB</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>tex</strong></p></td>
<td align="left"><p>D3DSIO_TEX</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>texcoord</strong></p></td>
<td align="left"><p>D3DSIO_TEXCOORD</p></td>
</tr>
</tbody>
</table>

 

请注意，在所有顶点着色器版本中， **子** 组装器指令是 \_ 使用源修饰符实现的 D3DSIO ADD 操作， (bits 27:24) 的第二个源设置为否定 (0x1) 。

**Tex** 和 **texcoord** 说明适用于像素着色器版本 1 \_ 0 到 1 \_ 3; 每个指令都有一个关联的 [目标参数](destination-parameter-token.md)。

**Texld** 和 **texcrd** 说明是像素着色器版本 1 4 及更高版本的新说明 \_ ; 每个指令都具有与之关联的目标和 [源参数](source-parameter-token.md)。

运行时将 **tex** 和 **texld** 组装器指令转换为 D3DSIO \_ tex 内核模式操作。 运行时将 **texcoord** 和 **texcrd** 组装器指令转换为 D3DSIO \_ texcoord 内核模式操作。 驱动程序首先验证着色器代码的像素着色器版本，然后相应地处理说明。 例如，如果驱动程序使用 D3DSIO TEX 操作验证它是否收到了版本 1 \_ 4 像素着色器代码 \_ ，则驱动程序将确定 destination 和 source 参数跟在指令标记之后。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

