---
title: .locale（指定区域设置）
description: Locale 命令设置区域设置或显示当前区域设置。
keywords:
- 。 (设置区域设置的区域设置) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .locale (Set Locale)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 806aa0855ae775652662b3e93ec1bb8755a2dc97
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829815"
---
# <a name="locale-set-locale"></a>.locale（指定区域设置）


**Locale** 命令设置区域设置或显示当前区域设置。

```dbgcmd
.locale [Locale] 
```

## <a name="span-idddk_meta_set_locale_dbgspanspan-idddk_meta_set_locale_dbgspanparameters"></a><span id="ddk_meta_set_locale_dbg"></span><span id="DDK_META_SET_LOCALE_DBG"></span>参数


<span id="_______Locale______"></span><span id="_______locale______"></span><span id="_______LOCALE______"></span>*区域设置*   
指定所需的区域设置。 如果省略此参数，则调试器将显示当前区域设置。

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关区域设置的详细信息，请参阅 **setlocale** 例程参考页。

<a name="remarks"></a>备注
-------

区域设置控制 Unicode 字符串的显示方式。

下面的示例演示了 **. locale** 命令。

```dbgcmd
kd> .locale
Locale: C

kd> .locale E
Locale: English_United States.1252

kd> .locale c
Locale: Catalan_Spain.1252

kd> .locale C
Locale: C
```

 

 





