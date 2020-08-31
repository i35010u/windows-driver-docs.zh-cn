---
title: DXVA_ConfigQueryOrReplyFlag 和 DXVA_ConfigQueryorReplyFunc
description: DXVA_ConfigQueryOrReplyFlag 和 DXVA_ConfigQueryorReplyFunc 变量
ms.assetid: bfb1a98e-b9f0-4baa-b486-b2ff33a8bac5
keywords:
- 视频解码 WDK DirectX VA，格式
- 解码视频 WDK DirectX VA，格式
- 图片解码 WDK DirectX VA，格式
- 格式化 WDK DirectX VA
- bDXVA_Func 变量 WDK DirectX VA
- DXVA_ConfigQueryOrReplyFlag
- DXVA_ConfigQueryorReplyFunc
- 视频解码 WDK DirectX VA，配置探测和锁定
- 解码视频 WDK DirectX VA，配置探测和锁定
- 图片解码 WDK DirectX VA，配置探测和锁定
- 最小互操作性配置集 WDK DirectX VA
- 锁定配置 WDK DirectX VA
- 探测配置 WDK DirectX VA
- 配置探测和锁定 WDK DirectX VA
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: c59c17b45d65ff24a11e1d3bffa8d90b514d66e0
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89064302"
---
# <a name="dxva_configqueryorreplyflag-and-dxva_configqueryorreplyfunc-variables"></a>DXVA \_ ConfigQueryOrReplyFlag 和 DXVA \_ ConfigQueryorReplyFunc 变量

*DXVA \_ ConfigQueryOrReplyFlag*变量指示使用探测和锁定命令时的查询或响应的类型。 以下结构的 **dwFunction** 成员的最高有效24位包含 *DXVA \_ ConfigQueryOrReplyFlag* 变量。

[**DXVA \_**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)用于压缩的图片解码的 ConfigPictureDecode。

[**DXVA \_ConfigAlphaLoad**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphaload) 用于 alpha 混合数据加载。

[**DXVA \_**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphacombine)用于 alpha 混合组合的 ConfigAlphaCombine。

*DXVA \_ ConfigQueryOrReplyFlag*变量最重要的20位指定以下查询和响应。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0xFFFF1</p></td>
<td align="left"><p>由主机解码器作为探测命令发送。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFF5</p></td>
<td align="left"><p>由主机解码器作为锁定命令发送。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFFFF8</p></td>
<td align="left"><p>由加速器发送的 S_OK 对探测命令的响应，以及探测的配置的副本。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFF9</p></td>
<td align="left"><p>由加速器发送的对探测命令 S_OK 响应，具有建议的备用配置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFFFFC</p></td>
<td align="left"><p>由加速器发送，其中包含锁定的配置副本的 S_OK 响应锁定命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFFB</p></td>
<td align="left"><p>由加速器发送的对探测命令 S_FALSE 响应，具有建议的备用配置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFFFFF</p></td>
<td align="left"><p>由加速器发送的对锁定命令的 S_FALSE 响应，带有建议的备用配置。</p></td>
</tr>
</tbody>
</table>

 

*DXVA \_ ConfigQueryOrReplyFlag*变量的最小有效4位为查询和响应指定以下状态指示器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">bit</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>当主机解码器发送时，此值为零，加速器发送时为1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>与探测相关联时，此值为零，而与锁关联时则为1。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>如果成功，则为零; 如果失败，则为1。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>如果它是重复的配置结构，则为零; 如果为新配置结构，则为1。</p></td>
</tr>
</tbody>
</table>

 

**DwFunction**成员的最不重要的8位是*bDXVA \_ Func*变量。 与*DXVA \_ ConfigQueryorReplyFunc*一起使用时， *bDXVA \_ Func*变量指示探测和锁定操作并指定关联的配置函数。

### <a name="span-idprobing_and_lockingspanspan-idprobing_and_lockingspanspan-idprobing_and_lockingspanprobing-and-locking"></a><span id="Probing_and_Locking"></span><span id="probing_and_locking"></span><span id="PROBING_AND_LOCKING"></span>探测和锁定

当使用*bDXVA \_ func*探测和锁定特定 DirectX VA 函数的配置时， *bDXVA \_ Func*会置于*DXVA* \_ *ConfigQueryorReplyFunc*变量的8个最小有效位。 *DXVA* \_*ConfigQueryorReplyFunc*会传达 Microsoft Windows SDK 中指定的快捷键。

### <a name="span-idspecifying_a_configuration_to_be_probed_or_lockedspanspan-idspecifying_a_configuration_to_be_probed_or_lockedspanspan-idspecifying_a_configuration_to_be_probed_or_lockedspanspecifying-a-configuration-to-be-probed-or-locked"></a><span id="Specifying_a_Configuration_To_Be_Probed_or_Locked"></span><span id="specifying_a_configuration_to_be_probed_or_locked"></span><span id="SPECIFYING_A_CONFIGURATION_TO_BE_PROBED_OR_LOCKED"></span>指定要探测或锁定的配置

当*使用 bDXVA \_ Func*指定与通过探测或 lock 命令传递的配置结构关联的函数时， *bDXVA \_ Func*将放置在以下配置结构之一的**dwFunction**成员的*DXVA \_ ConfigQueryorReplyFunc*变量的8个最小有效位中：

[**DXVA \_**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)用于压缩的图片解码的 ConfigPictureDecode。

[**DXVA \_ConfigAlphaLoad**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphaload) 用于 alpha 混合数据加载。

[**DXVA \_**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphacombine)用于 alpha 混合组合的 ConfigAlphaCombine。

### <a name="span-iddxva_encryptprotocolfuncspanspan-iddxva_encryptprotocolfuncspanspan-iddxva_encryptprotocolfuncspandxva_encryptprotocolfunc"></a><span id="DXVA_EncryptProtocolFunc"></span><span id="dxva_encryptprotocolfunc"></span><span id="DXVA_ENCRYPTPROTOCOLFUNC"></span>DXVA \_ EncryptProtocolFunc

*DXVA \_ EncryptProtocolFunc* DWORD 变量的最高有效24位设置如下：

-   0xFFFF00 在调用[*DdMoCompRender*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)的[**DD \_ RENDERMOCOMPDATA**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构的**dwFunction**成员中由主机软件解码器发送时。

-   0xFFFF08 由视频加速器在[**DXVA \_ EncryptProtocolHeader**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_encryptprotocolheader)结构的**dwFunction**成员中发送。

*DXVA \_ EncryptProtocolFunc* DWORD 变量的最低有效8位包含与加密协议关联的*bDXVA \_ Func*的值。 此使用支持的唯一值是 *bDXVA \_ Func* = 1 (压缩的图片解码) 。

### <a name="span-idspecifying_an_operation_to_be_performed_by_ddmocomprenderspanspan-idspecifying_an_operation_to_be_performed_by_ddmocomprenderspanspan-idspecifying_an_operation_to_be_performed_by_ddmocomprenderspanspecifying-an-operation-to-be-performed-by-ddmocomprender"></a><span id="Specifying_an_Operation_to_be_Performed_by_DdMoCompRender"></span><span id="specifying_an_operation_to_be_performed_by_ddmocomprender"></span><span id="SPECIFYING_AN_OPERATION_TO_BE_PERFORMED_BY_DDMOCOMPRENDER"></span>指定 DdMoCompRender 执行的操作

当使用*bDXVA \_ func*来指示要执行的实际操作 (压缩的图片解码、alpha 混合数据加载、alpha 混合组合或图片重新采样) 时，通过在对[*RENDERMOCOMPDATA*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)的调用中，将*bDXVA \_ Func*包含在[**DD \_ DdMoCompRender**](/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构的**dwFunction**成员的一系列*bDXVA \_ Func*字节值中。 第一个 *bDXVA \_ Func* 操作是在最重要的字节中指定的，下一个操作是在下一个最重要的字节中指定的，依此类推。 **DwFunction**的剩余字节数设置为零。

 

