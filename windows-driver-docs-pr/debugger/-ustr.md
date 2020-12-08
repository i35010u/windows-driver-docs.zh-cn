---
title: ustr
description: Ustr 扩展显示 UNICODE_STRING 结构。
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
ms.openlocfilehash: 7f52becf1253a6660ff56fbec23e899896272bd8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833853"
---
# <a name="ustr"></a>!ustr


**！ Ustr** EXTENSION 显示 UNICODE \_ 字符串结构。

```dbgcmd
!ustr Address
```

## <a name="span-idddk__ustr_dbgspanspan-idddk__ustr_dbgspanparameters"></a><span id="ddk__ustr_dbg"></span><span id="DDK__USTR_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 UNICODE 字符串结构的十六进制地址 \_ 。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 UNICODE 字符串结构的详细信息 \_ ，请参阅 Microsoft Windows SDK 文档。

<a name="remarks"></a>备注
-------

Unicode 字符串被计算为16位字符字符串，如以下结构中所定义：

```cpp
typedef struct _UNICODE_STRING {
    USHORT Length;
    USHORT MaximumLength;
    PWSTR  Buffer;
} UNICODE_STRING;
```

如果字符串以 null 结尾，则 **长度** 不包含尾随 null。

大多数 Win32 字符串参数在完成任何实际工作之前都将转换为 Unicode 字符串。

 

 





