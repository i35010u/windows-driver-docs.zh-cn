---
title: obja
description: Obja 扩展在对象管理器中显示对象的属性。
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
ms.openlocfilehash: 6ae728050e5e3b443814a40fc0a924a043614895
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819413"
---
# <a name="obja"></a>!obja


**！ Obja** 扩展在对象管理器中显示对象的属性。

```dbgcmd
!obja Address
```

## <a name="span-idddk__obja_dbgspanspan-idddk__obja_dbgspanparameters"></a><span id="ddk__obja_dbg"></span><span id="DDK__OBJA_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定要检查的对象标头的十六进制地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关对象和对象管理器的信息，请参阅 Microsoft Windows SDK 文档、Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，Mark Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

列出了与指定的对象相关的属性。 有效的属性包括：

```cpp
#define OBJ_INHERIT             0x00000002L
#define OBJ_PERMANENT           0x00000010L
#define OBJ_EXCLUSIVE           0x00000020L
#define OBJ_CASE_INSENSITIVE    0x00000040L
#define OBJ_OPENIF              0x00000080L
#define OBJ_OPENLINK            0x00000100L
#define OBJ_VALID_ATTRIBUTES    0x000001F2L
```

以下是示例：

```dbgcmd
kd> !obja 80967768
Obja +80967768 at 80967768:
        OBJ_INHERIT
        OBJ_PERMANENT
        OBJ_EXCLUSIVE
```

 

 





