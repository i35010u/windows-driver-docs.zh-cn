---
title: ustr
description: Ustr 扩展显示 UNICODE_STRING 结构。
ms.assetid: 17b84bf0-5a5b-47a5-893b-fdc58ca2afc3
keywords:
- 字符串
- UNICODE_STRING 结构
- ustr Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ustr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3edcbc657def7230ee0b7ca0488c542b227a0751
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554151"
---
# <a name="ustr"></a>！ ustr


**！ Ustr**扩展插件都会显示 UNICODE\_字符串结构。

```dbgcmd
!ustr Address
```

## <a name="span-idddkustrdbgspanspan-idddkustrdbgspanparameters"></a><span id="ddk__ustr_dbg"></span><span id="DDK__USTR_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定 UNICODE 的十六进制地址\_字符串结构。

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

有关 UNICODE 的详细信息\_字符串结构，请参阅 Microsoft Windows SDK 文档。

<a name="remarks"></a>备注
-------

Unicode 字符串被计算在内 16 位字符字符串，如以下结构中定义：

```cpp
typedef struct _UNICODE_STRING {
    USHORT Length;
    USHORT MaximumLength;
    PWSTR  Buffer;
} UNICODE_STRING;
```

如果字符串以 null 结尾**长度**不包括尾随的 null。

完成任何实际工作之前，大多数的 Win32 字符字符串自变量将转换为 Unicode 字符串。

 

 





