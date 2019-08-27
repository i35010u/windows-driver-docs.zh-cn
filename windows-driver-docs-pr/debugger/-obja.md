---
title: obja
description: Obja 扩展在对象管理器中显示对象的属性。
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
ms.openlocfilehash: 56afcda226e8e242a5b61aa96df777ecd1815f91
ms.sourcegitcommit: 424c435700d8f8a85bdaa83e8ddaab9568c8d347
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/26/2019
ms.locfileid: "70025203"
---
# <a name="obja"></a>!obja


**! Obja**扩展在对象管理器中显示对象的属性。

```dbgcmd
!obja Address
```

## <a name="span-idddk__obja_dbgspanspan-idddk__obja_dbgspanparameters"></a><span id="ddk__obja_dbg"></span><span id="DDK__OBJA_DBG"></span>Parameters


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
Ext .dll Kdextx86</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 和更高版本</strong></p></td>
<td align="left"><p>Ext .dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关对象和对象管理器的信息, 请参阅 "Microsoft Windows SDK 文档"、"Windows 驱动程序工具包 (WDK)" 文档, 以及 " *Microsoft Windows 内部*" (Russinovich) 和 "David 所罗门群岛"。

<a name="remarks"></a>备注
-------

列出了与指定的对象相关的属性。 有效的属性包括:

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

 

 





