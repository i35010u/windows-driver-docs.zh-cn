---
title: 指令令牌
description: 指令令牌
ms.assetid: bfeee1ad-aaf3-41d0-a667-15d22eccd1e9
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: 91cbfeb2201b6c715617b2cbe5d6304476fe3f41
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533141"
---
# <a name="instruction-token"></a>指令令牌


## <span id="ddk_instruction_token_gg"></span><span id="DDK_INSTRUCTION_TOKEN_GG"></span>


指令令牌告知要执行特定操作的驱动程序，并由组成以下位：

### <a name="span-idbitsspanspan-idbitsspanbits"></a><span id="bits"></span><span id="BITS"></span>Bits

<span id="_15_00_"></span>**\[15:00\]**  0 到 15 位指示[操作代码](https://msdn.microsoft.com/library/windows/hardware/ff569706)。 D3DSIO\_ \*举例说明一个操作代码，其中\*表示指令。 例如，下面的代码片段演示[ADD 指令](https://msdn.microsoft.com/library/windows/hardware/ff538212):

```cpp
// D3DSIO_ADD d, s1, s2
```

<span id="_23_16_"></span>**\[23:16\]** 位 16 到 23 表示与操作代码相关的特定控件。

<span id="_27_24_"></span>**\[27:24\]** 早于 2 像素和顶点着色器版本\_0，24 到 27 位是保留和设为 0x0。

对于像素和顶点着色器版本 2\_0 和更高版本，位 24 到 27 指令不包括指令令牌本身 （即，包含指令不包括指令令牌的令牌的数） 的 dword 值中指定的大小。

<span id="_28_"></span>**\[28\]** 早于 2 像素和顶点着色器版本\_0，位 28 是保留，设为 0x0。

对于像素和顶点着色器版本 2\_0 和更高版本，位 28 指示是否的前提是该指令 （即，包含额外谓词源令牌的着色器代码的末尾。 如果此位设置为 0x1 的前提是该指令。

<span id="_29_"></span>**\[29\]** 保留。 此值设置为 0x0。

<span id="_30_"></span>**\[30\]** 像素着色器版本早于 2\_0，30 位是位的共同问题。 如果设置为 1，请执行前面的说明; 此指令否则，单独执行。

像素着色器版本 2\_0 和更高版本和所有顶点着色器版本中，保留 30 位并将其设为 0x0。

<span id="_31_"></span>**\[31\]** 位 31 是零 (0x0)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

有关可以在 0 到 15 个指令令牌位中指定的操作的详细信息的最新的 DirectX SDK 文档中，请参阅像素着色器引用和顶点着色器引用。

DirectX3D 运行时从应用程序收到着色器代码后，运行时的代码传递到驱动程序之前会验证代码。 通常情况下，运行时添加前缀组装器说明与"D3DSIO\_"若要创建在操作代码。 例如，下面的组装器说明对应于内核模式操作：

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

 

请注意，在所有顶点着色器版本中， **sub**汇编程序指令实现为 D3DSIO\_添加操作使用源修饰符 (位 27:24) 的第二个源设置为负号 (0x1)。

**Tex**并**texcoord**说明适用于像素着色器版本 1\_0 到 1 之间\_3; 每个指令具有一个[destination 参数](destination-parameter-token.md)与之关联。

**Texld**并**texcrd**说明不熟悉像素着色器版本 1\_4 及更高版本; 每个指令有两个目标和[源参数](source-parameter-token.md)与之关联。

在运行时将转换**tex**并**texld** D3DSIO 组装器说明\_TEX 内核模式操作。 在运行时将转换**texcoord**并**texcrd** D3DSIO 组装器说明\_TEXCOORD 内核模式操作。 驱动程序首先验证着色器代码的像素着色器版本，然后相应地处理说明。 例如，如果驱动程序验证了 it 收到版本 1\_4 像素着色器代码使用 D3DSIO\_TEX 操作，该驱动程序确定目标和源参数按照指令令牌。

## <a name="span-idrequirementsspanspan-idrequirementsspanspan-idrequirementsspanrequirements"></a><span id="Requirements"></span><span id="requirements"></span><span id="REQUIREMENTS"></span>要求


在 Windows Vista 和更高版本的 Windows 操作系统中可用。

 

 





