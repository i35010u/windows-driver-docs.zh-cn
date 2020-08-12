---
title: dg（显示选择器）
description: Dg 命令显示指定选择器的段说明符。
ms.assetid: bf680931-f4f9-4b72-bb25-42d095514d2a
keywords:
- ) Windows 调试的 dg (显示选择器
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dg (Display Selector)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c61d74020b56131dd3b472e077fe86f47b835842
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148495"
---
# <a name="dg-display-selector"></a>dg（显示选择器）


**Dg**命令显示指定选择器的段说明符。

```dbgcmd
dg FirstSelector [LastSelector]
```

## <a name="span-idddk_cmd_display_selector_dbgspanspan-idddk_cmd_display_selector_dbgspanparameters"></a><span id="ddk_cmd_display_selector_dbg"></span><span id="DDK_CMD_DISPLAY_SELECTOR_DBG"></span>参数


<span id="_______FirstSelector______"></span><span id="_______firstselector______"></span><span id="_______FIRSTSELECTOR______"></span>*FirstSelector*   
指定要显示的第一个选择器的十六进制选择器值。

<span id="_______LastSelector______"></span><span id="_______lastselector______"></span><span id="_______LASTSELECTOR______"></span>*LastSelector*   
指定要显示的最后一个选择器的十六进制选择器值。 如果省略此项，则只显示一个选择器。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>x86</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此命令不能显示超过256个选择器。

常用选择器值包括：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ID</th>
<th align="left">Decimal</th>
<th align="left">hex</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>KGDT_NULL</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0x00</p></td>
</tr>
<tr class="even">
<td align="left"><p>KGDT_R0_CODE</p></td>
<td align="left"><p>8</p></td>
<td align="left"><p>0x08</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KGDT_R0_DATA</p></td>
<td align="left"><p>16</p></td>
<td align="left"><p>0x10</p></td>
</tr>
<tr class="even">
<td align="left"><p>KGDT_R3_CODE</p></td>
<td align="left"><p>24</p></td>
<td align="left"><p>0x18</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KGDT_R3_DATA</p></td>
<td align="left"><p>32</p></td>
<td align="left"><p>0x20</p></td>
</tr>
<tr class="even">
<td align="left"><p>KGDT_TSS</p></td>
<td align="left"><p>40</p></td>
<td align="left"><p>0x28</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KGDT_R0_PCR</p></td>
<td align="left"><p>48</p></td>
<td align="left"><p>0x30</p></td>
</tr>
<tr class="even">
<td align="left"><p>KGDT_R3_TEB</p></td>
<td align="left"><p>56</p></td>
<td align="left"><p>0x38</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KGDT_VDM_TILE</p></td>
<td align="left"><p>64</p></td>
<td align="left"><p>0x40</p></td>
</tr>
<tr class="even">
<td align="left"><p>KGDT_LDT</p></td>
<td align="left"><p>72</p></td>
<td align="left"><p>0x48</p></td>
</tr>
<tr class="odd">
<td align="left"><p>KGDT_DF_TSS</p></td>
<td align="left"><p>80</p></td>
<td align="left"><p>0x50</p></td>
</tr>
<tr class="even">
<td align="left"><p>KGDT_NMI_TSS</p></td>
<td align="left"><p>88</p></td>
<td align="left"><p>0x58</p></td>
</tr>
</tbody>
</table>

 

 

 





