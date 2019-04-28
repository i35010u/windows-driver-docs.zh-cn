---
title: obja
description: Obja 扩展对象管理器中显示的对象的属性。
ms.assetid: dc263ec2-72bf-4cb1-8583-4e9142d0bbdb
keywords:
- 对象管理器
- obja Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- obja
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ca660e5a95b68af9766bb8c9c1e2e9ddb484161f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335828"
---
# <a name="obja"></a>!obja


**！ Obja**扩展对象管理器中显示的对象的属性。

```dbgcmd
!obja Address
```

## <a name="span-idddkobjadbgspanspan-idddkobjadbgspanparameters"></a><span id="ddk__obja_dbg"></span><span id="DDK__OBJA_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定你想要检查的对象标头的十六进制地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Ext.dll Kdextx86.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ext.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关对象和对象管理器的信息，请参阅 Microsoft Windows SDK 文档，Windows Driver Kit (WDK) 文档，并*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

列出与指定的对象相关的属性。 有效的属性是：

```cpp
#define OBJ_INHERIT             0x00000002L
#define OBJ_PERMANENT           0x00000010L
#define OBJ_EXCLUSIVE           0x00000020L
#define OBJ_CASE_INSENSITIVE    0x00000040L
#define OBJ_OPENIF              0x00000080L
#define OBJ_OPENLINK            0x00000100L
#define OBJ_VALID_ATTRIBUTES    0x000001F2L
```

下面是一个示例：

```dbgcmd
kd> !obja 80967768
Obja +80967768 at 80967768:
        OBJ_INHERIT
        OBJ_PERMANENT
        OBJ_EXCLUSIVE
```

 

 





