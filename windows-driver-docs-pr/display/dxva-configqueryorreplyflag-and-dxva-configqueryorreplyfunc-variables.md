---
title: DXVA_ConfigQueryOrReplyFlag 和 DXVA_ConfigQueryorReplyFunc
description: DXVA_ConfigQueryOrReplyFlag 和 DXVA_ConfigQueryorReplyFunc 变量
ms.assetid: bfb1a98e-b9f0-4baa-b486-b2ff33a8bac5
keywords:
- 视频解码 WDK DirectX VA，格式
- 解码视频 WDK DirectX VA，格式
- 解码 WDK DirectX va，因此格式的图片
- 格式 WDK DirectX VA
- bDXVA_Func 变量 WDK DirectX VA
- DXVA_ConfigQueryOrReplyFlag
- DXVA_ConfigQueryorReplyFunc
- 视频解码 WDK DirectX va，因此配置探测和锁定
- 解码视频 WDK DirectX va，因此配置探测和锁定
- 解码 WDK DirectX va，因此配置探测和锁定的图片
- 最小互操作性配置设置 WDK DirectX VA
- 锁定配置 WDK DirectX VA
- 探测配置 WDK DirectX VA
- 配置探测和锁定 WDK DirectX VA
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 68d0c0727156b80ffac718897cd1e3e9d1b8a6e5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370817"
---
# <a name="dxvaconfigqueryorreplyflag-and-dxvaconfigqueryorreplyfunc-variables"></a>DXVA\_ConfigQueryOrReplyFlag 和 DXVA\_ConfigQueryorReplyFunc 变量

*DXVA\_ConfigQueryOrReplyFlag*变量指示查询的类型或使用探测和锁定时的响应的命令。 最重要的 24 字节**dwFunction**以下结构的成员包含*DXVA\_ConfigQueryOrReplyFlag*变量。

[**DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)用于压缩的图片解码。

[**DXVA\_ConfigAlphaLoad** ](https://msdn.microsoft.com/library/windows/hardware/ff563129)的 alpha 值混合处理数据。

[**DXVA\_ConfigAlphaCombine** ](https://msdn.microsoft.com/library/windows/hardware/ff563126) alpha 值混合处理组合。

最明显的 20 位*DXVA\_ConfigQueryOrReplyFlag*变量指定以下查询和响应。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0xFFFF1</p></td>
<td align="left"><p>由主机解码器将作为发送探测的命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFF5</p></td>
<td align="left"><p>由主机解码器发送作为锁定命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFFFF8</p></td>
<td align="left"><p>发送到探测的命令，以探测模式配置的副本，则为 S_OK 响应快捷键的命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFF9</p></td>
<td align="left"><p>发送到具有建议的替代配置的探测命令，则为 S_OK 响应快捷键的命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFFFFC</p></td>
<td align="left"><p>发送到锁定的命令，使用的锁定配置副本，则为 S_OK 响应快捷键的命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFFB</p></td>
<td align="left"><p>由 S_FALSE 响应探测的命令，使用建议的替代配置到加速器发送。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFFFFF</p></td>
<td align="left"><p>发送到锁定的命令，使用建议的替代配置 S_FALSE 响应快捷键的命令。</p></td>
</tr>
</tbody>
</table>

 

最低有效位的 4 位*DXVA\_ConfigQueryOrReplyFlag*变量指定查询和响应的以下状态指示符。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">位</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>该值为 0 时发送的主机解码器和 1 时发送的快捷键。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>该值为 0 时与探测程序和与锁相关的 1 相关联。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>这是成功，0，1 表示失败。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>它是一个重复的配置结构和 1 时是新的配置结构时，这是零。</p></td>
</tr>
</tbody>
</table>

 

最明显的 8 位**dwFunction**成员是是*bDXVA\_Func*变量。 *BDXVA\_Func*变量，与一起使用时*DXVA\_ConfigQueryorReplyFunc*、 指示探测和锁定操作，并指定关联的配置函数。

### <a name="span-idprobingandlockingspanspan-idprobingandlockingspanspan-idprobingandlockingspanprobing-and-locking"></a><span id="Probing_and_Locking"></span><span id="probing_and_locking"></span><span id="PROBING_AND_LOCKING"></span>探测和锁定

当*bDXVA\_Func*用于探测，锁定对于特定的 DirectX VA 函数，配置*bDXVA\_Func*置于8最低有效位*DXVA*\_*ConfigQueryorReplyFunc*变量。 *DXVA*\_*ConfigQueryorReplyFunc*传达给 Microsoft Windows SDK 中指定的快捷键。

### <a name="span-idspecifyingaconfigurationtobeprobedorlockedspanspan-idspecifyingaconfigurationtobeprobedorlockedspanspan-idspecifyingaconfigurationtobeprobedorlockedspanspecifying-a-configuration-to-be-probed-or-locked"></a><span id="Specifying_a_Configuration_To_Be_Probed_or_Locked"></span><span id="specifying_a_configuration_to_be_probed_or_locked"></span><span id="SPECIFYING_A_CONFIGURATION_TO_BE_PROBED_OR_LOCKED"></span>指定要探测或锁定的配置

当*bDXVA\_Func*用于指定与配置结构传递使用探测或 lock 命令时，关联的函数*bDXVA\_Func*置于 8最高有效位*DXVA\_ConfigQueryorReplyFunc*变量中**dwFunction**之一的以下配置结构的成员：

[**DXVA\_ConfigPictureDecode** ](https://msdn.microsoft.com/library/windows/hardware/ff563133)用于压缩的图片解码。

[**DXVA\_ConfigAlphaLoad** ](https://msdn.microsoft.com/library/windows/hardware/ff563129)的 alpha 值混合处理数据。

[**DXVA\_ConfigAlphaCombine** ](https://msdn.microsoft.com/library/windows/hardware/ff563126) alpha 值混合处理组合。

### <a name="span-iddxvaencryptprotocolfuncspanspan-iddxvaencryptprotocolfuncspanspan-iddxvaencryptprotocolfuncspandxvaencryptprotocolfunc"></a><span id="DXVA_EncryptProtocolFunc"></span><span id="dxva_encryptprotocolfunc"></span><span id="DXVA_ENCRYPTPROTOCOLFUNC"></span>DXVA\_EncryptProtocolFunc

最重要的 24 字节*DXVA\_EncryptProtocolFunc* DWORD 变量设置，如下所示：

-   0xFFFF00 时发送的中的主机软件解码器**dwFunction**的成员[ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)中调用的结构[*DdMoCompRender*](https://msdn.microsoft.com/library/windows/hardware/ff550248)。

-   通过中的视频加速服务发送时 0xFFFF08 **dwFunction**的成员[ **DXVA\_EncryptProtocolHeader** ](https://msdn.microsoft.com/library/windows/hardware/ff563965)结构。

最明显的 8 位*DXVA\_EncryptProtocolFunc* DWORD 变量包含的值*bDXVA\_Func*加密协议与相关联。 为此，请使用支持的唯一值*bDXVA\_Func* = 1 （压缩的图片解码）。

### <a name="span-idspecifyinganoperationtobeperformedbyddmocomprenderspanspan-idspecifyinganoperationtobeperformedbyddmocomprenderspanspan-idspecifyinganoperationtobeperformedbyddmocomprenderspanspecifying-an-operation-to-be-performed-by-ddmocomprender"></a><span id="Specifying_an_Operation_to_be_Performed_by_DdMoCompRender"></span><span id="specifying_an_operation_to_be_performed_by_ddmocomprender"></span><span id="SPECIFYING_AN_OPERATION_TO_BE_PERFORMED_BY_DDMOCOMPRENDER"></span>指定要由 DdMoCompRender 执行操作

当*bDXVA\_Func*用于发出信号要执行的实际操作 （压缩图片解码、 alpha 混合数据加载、 alpha 混合组合或图片来重新采样） *bDXVA\_Func*由包含在一系列中传达给快捷键*bDXVA\_Func*中的字节值**dwFunction**的成员[ **DD\_RENDERMOCOMPDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551693)对的调用中的结构[ *DdMoCompRender*](https://msdn.microsoft.com/library/windows/hardware/ff550248)。 第一个*bDXVA\_Func*中最高有效字节指定操作，则下一步操作中指定的下一步最高有效字节，依此类推。 任何剩余字节数**dwFunction**设置为零。

 

 





