---
title: .locale（指定区域设置）
description: .Locale 命令会将区域设置，或显示当前区域设置。
ms.assetid: 66c2a522-886f-41ef-ab90-176a3e0b7d88
keywords:
- .locale （设置区域设置） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .locale (Set Locale)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 39cc03ebcdc74b86e7d471cccc62583a55d20186
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567564"
---
# <a name="locale-set-locale"></a>.locale（指定区域设置）


**.Locale**命令会将区域设置或显示当前区域设置。

```dbgcmd
.locale [Locale] 
```

## <a name="span-idddkmetasetlocaledbgspanspan-idddkmetasetlocaledbgspanparameters"></a><span id="ddk_meta_set_locale_dbg"></span><span id="DDK_META_SET_LOCALE_DBG"></span>参数


<span id="_______Locale______"></span><span id="_______locale______"></span><span id="_______LOCALE______"></span> *区域设置*   
指定所需的区域设置。 如果省略此参数时，调试器将显示当前区域设置。

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
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关区域设置的详细信息，请参阅**setlocale**日常参考页。

<a name="remarks"></a>备注
-------

区域设置控制如何显示 Unicode 字符串。

下面的示例演示 **.locale**命令。

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

 

 





