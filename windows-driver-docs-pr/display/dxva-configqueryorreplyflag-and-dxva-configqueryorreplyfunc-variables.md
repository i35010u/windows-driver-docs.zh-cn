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
ms.openlocfilehash: 08309fc27a221f0184f12dcced5be49106443d01
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838971"
---
# <a name="dxva_configqueryorreplyflag-and-dxva_configqueryorreplyfunc-variables"></a>DXVA\_ConfigQueryOrReplyFlag 和 DXVA\_ConfigQueryorReplyFunc 变量

当使用探测和锁定命令时， *DXVA\_ConfigQueryOrReplyFlag*变量指示查询或响应的类型。 以下结构的**dwFunction**成员的最高有效24位包含*DXVA\_ConfigQueryOrReplyFlag*变量。

[**DXVA\_ConfigPictureDecode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)用于压缩的图片解码。

用于 alpha 混合数据加载的[**DXVA\_ConfigAlphaLoad**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphaload) 。

用于 alpha 混合组合的[**DXVA\_ConfigAlphaCombine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphacombine) 。

DXVA 的最重要20位 *\_ConfigQueryOrReplyFlag*变量指定以下查询和响应。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Value</th>
<th align="left">描述</th>
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
<td align="left"><p>由加速器发送，其中包含已探测配置的副本响应探测命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFF9</p></td>
<td align="left"><p>由加速器发送并带有建议的替代配置的 S_OK 响应发送到探测命令。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFFFFC</p></td>
<td align="left"><p>由加速器发送，其中包含锁定的配置副本的对锁定命令的 S_OK 响应。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xFFFFB</p></td>
<td align="left"><p>由加速器发送的对探测命令的 S_FALSE 响应发送，具有建议的可选配置。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xFFFFF</p></td>
<td align="left"><p>由加速器发送，其中包含一个建议的替代配置，其中包含对锁定命令的 S_FALSE 响应。</p></td>
</tr>
</tbody>
</table>

 

*DXVA\_ConfigQueryOrReplyFlag*变量的最小有效4位为查询和响应指定以下状态指示器。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">小段</th>
<th align="left">描述</th>
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

 

**DwFunction**成员的最不重要的8位是*bDXVA\_Func*变量。 *BDXVA\_函数*与*DXVA\_ConfigQueryorReplyFunc*一起使用时，指示探测和锁定操作并指定关联的配置函数。

### <a name="span-idprobing_and_lockingspanspan-idprobing_and_lockingspanspan-idprobing_and_lockingspanprobing-and-locking"></a><span id="Probing_and_Locking"></span><span id="probing_and_locking"></span><span id="PROBING_AND_LOCKING"></span>探测和锁定

当*bDXVA\_Func*用于探测和锁定特定 DirectX VA 函数的配置时， *bDXVA\_Func*会置于*DXVA*\_*ConfigQueryorReplyFunc*变量的8个最小有效位。 *DXVA*\_*ConfigQueryorReplyFunc*会传达 Microsoft Windows SDK 中指定的快捷键。

### <a name="span-idspecifying_a_configuration_to_be_probed_or_lockedspanspan-idspecifying_a_configuration_to_be_probed_or_lockedspanspan-idspecifying_a_configuration_to_be_probed_or_lockedspanspecifying-a-configuration-to-be-probed-or-locked"></a><span id="Specifying_a_Configuration_To_Be_Probed_or_Locked"></span><span id="specifying_a_configuration_to_be_probed_or_locked"></span><span id="SPECIFYING_A_CONFIGURATION_TO_BE_PROBED_OR_LOCKED"></span>指定要探测或锁定的配置

当使用*bDXVA\_Func*来指定与通过探测或 lock 命令传递的配置结构相关联的函数时， *bDXVA\_Func*会置于 DXVA 的8个最低有效位 *\_* 以下配置结构之一的**dwFunction**成员中的 ConfigQueryorReplyFunc 变量：

[**DXVA\_ConfigPictureDecode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configpicturedecode)用于压缩的图片解码。

用于 alpha 混合数据加载的[**DXVA\_ConfigAlphaLoad**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphaload) 。

用于 alpha 混合组合的[**DXVA\_ConfigAlphaCombine**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_configalphacombine) 。

### <a name="span-iddxva_encryptprotocolfuncspanspan-iddxva_encryptprotocolfuncspanspan-iddxva_encryptprotocolfuncspandxva_encryptprotocolfunc"></a><span id="DXVA_EncryptProtocolFunc"></span><span id="dxva_encryptprotocolfunc"></span><span id="DXVA_ENCRYPTPROTOCOLFUNC"></span>DXVA\_EncryptProtocolFunc

*DXVA\_EncryptProtocolFunc* DWORD 变量的最高有效24位设置如下：

-   0xFFFF00 在调用[*DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)的**dwFunction**成员中，由主机软件解码器发送到[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构。

-   0xFFFF08 由视频加速器在[**DXVA\_EncryptProtocolHeader**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_encryptprotocolheader)结构的**dwFunction**成员中发送。

*DXVA\_EncryptProtocolFunc* DWORD 变量的最低有效8位包含与加密协议关联的*bDXVA\_Func*的值。 此使用支持的唯一值是*bDXVA\_Func* = 1 （压缩图片解码）。

### <a name="span-idspecifying_an_operation_to_be_performed_by_ddmocomprenderspanspan-idspecifying_an_operation_to_be_performed_by_ddmocomprenderspanspan-idspecifying_an_operation_to_be_performed_by_ddmocomprenderspanspecifying-an-operation-to-be-performed-by-ddmocomprender"></a><span id="Specifying_an_Operation_to_be_Performed_by_DdMoCompRender"></span><span id="specifying_an_operation_to_be_performed_by_ddmocomprender"></span><span id="SPECIFYING_AN_OPERATION_TO_BE_PERFORMED_BY_DDMOCOMPRENDER"></span>指定 DdMoCompRender 执行的操作

当使用*bDXVA\_Func*来表示要执行的实际操作（压缩的图片解码、alpha 混合数据加载、alpha 混合组合或图像重新采样）， *bDXVA\_Func*将通过在对[*DdMoCompRender*](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_mocompcb_render)的调用中，包含在[**DD\_RENDERMOCOMPDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_rendermocompdata)结构的**dwFunction**成员中的一系列 *\_bDXVA*中。 第一个*bDXVA\_Func*操作是在最重要的字节中指定的，下一个操作是在下一个最重要的字节中指定，依此类推。 **DwFunction**的剩余字节数设置为零。

 

 





