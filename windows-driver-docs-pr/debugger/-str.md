---
title: str
description: Str 扩展显示 ANSI_STRING 或 OEM_STRING 结构。
ms.assetid: 5ebb29d4-5d77-475b-ace5-8bc8a4299320
keywords:
- 字符串
- ANSI_STRING 结构
- str Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- str
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1840a0ec00d167fdf87d9d02031152738417176c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520693"
---
# <a name="str"></a>!str


**！ Str**扩展插件都会显示 ANSI\_字符串或 OEM\_字符串结构。

```dbgcmd
!str Address
```

## <a name="span-idddkstrdbgspanspan-idddkstrdbgspanparameters"></a><span id="ddk__str_dbg"></span><span id="DDK__STR_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定 ANSI 的十六进制地址\_字符串或 OEM\_字符串结构。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关 ANSI\_字符串结构，请参阅 Microsoft Windows SDK 文档。

<a name="remarks"></a>备注
-------

ANSI 字符串被计算在内 8 位字符字符串，如以下结构中定义：

```cpp
typedef struct _STRING {
    USHORT Length;
    USHORT MaximumLength;
    PCHAR Buffer;
} STRING;
typedef STRING ANSI_STRING;
typedef STRING OEM_STRING;
```

如果字符串以 null 结尾**长度**不包括尾随的 null。

 

 





