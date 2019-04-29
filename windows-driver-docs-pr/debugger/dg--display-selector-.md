---
title: dg（显示选择器）
description: Dg 命令显示指定的选择器的段描述符。
ms.assetid: bf680931-f4f9-4b72-bb25-42d095514d2a
keywords:
- dg （显示选择器） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dg (Display Selector)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e4e0bc8c6e5795c8762a371b63732361aa5cf354
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324567"
---
# <a name="dg-display-selector"></a>dg（显示选择器）


**Dg**命令显示指定的选择器的段描述符。

```dbgcmd
dg FirstSelector [LastSelector]
```

## <a name="span-idddkcmddisplayselectordbgspanspan-idddkcmddisplayselectordbgspanparameters"></a><span id="ddk_cmd_display_selector_dbg"></span><span id="DDK_CMD_DISPLAY_SELECTOR_DBG"></span>参数


<span id="_______FirstSelector______"></span><span id="_______firstselector______"></span><span id="_______FIRSTSELECTOR______"></span> *FirstSelector*   
指定要显示的第一个选择器的十六进制选择器值。

<span id="_______LastSelector______"></span><span id="_______lastselector______"></span><span id="_______LASTSELECTOR______"></span> *LastSelector*   
指定要显示的最后一个选择器的十六进制选择器值。 如果省略此属性，将显示一个选择器。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>x86、 Itanium</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以通过此命令显示不超过 256 个选择器。

常见的选择器值为：

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ID</th>
<th align="left">十进制</th>
<th align="left">十六进制</th>
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

 

 

 





