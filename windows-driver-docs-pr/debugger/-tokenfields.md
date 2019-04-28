---
title: tokenfields
description: Tokenfields 扩展显示名称和访问令牌对象 （标记结构） 中的字段的偏移量。
ms.assetid: dfadfdb0-1ed8-4c21-9207-dc02d7435475
keywords:
- 令牌
- tokenfields Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- tokenfields
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1d0e0e7574e229e8edb9b26fc7f9d0eea43628b7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339820"
---
# <a name="tokenfields"></a>!tokenfields


**！ Tokenfields**扩展显示名称和访问令牌对象 （标记结构） 中的字段的偏移量。

```dbgcmd
!tokenfields
```

## <span id="ddk__tokenfields_dbg"></span><span id="DDK__TOKENFIELDS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>不可用 （请参阅备注部分）</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

标记结构有关的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。 本书可能在某些语言和国家/地区中可用。（Microsoft Windows SDK 文档中所述的用户模式下令牌结构稍有不同。）

<a name="remarks"></a>备注
-------

此扩展命令不可在 Windows XP 或更高版本的 Windows 中可用。 请改用[ **dt （显示类型）** ](dt--display-type-.md)命令直接显示标记结构：

```dbgcmd
kd> dt nt!_TOKEN 
```

若要查看标记结构的特定实例，请使用[ **！ 令牌**](-token.md)扩展。

下面是举例 **！ tokenfields**从 Windows 2000 系统：

```dbgcmd
kd> !tokenfields
 TOKEN structure offsets:
    TokenSource:           0x0
    AuthenticationId:      0x18
    ExpirationTime:        0x28
    ModifiedId:            0x30
    UserAndGroupCount:     0x3c
    PrivilegeCount:        0x44
    VariableLength:        0x48
    DynamicCharged:        0x4c
    DynamicAvailable:      0x50
    DefaultOwnerIndex:     0x54
    DefaultDacl:           0x6c
    TokenType:             0x70
    ImpersonationLevel:    0x74
    TokenFlags:            0x78
    TokenInUse:            0x79
 ProxyData:             0x7c
    AuditData:             0x80
    VariablePart:          0x84
```

 

 





