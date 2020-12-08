---
title: tokenfields
description: Tokenfields 扩展显示 (令牌结构) 的访问令牌对象中的字段的名称和偏移量。
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
ms.openlocfilehash: d5193f1e11aa3113e64aa1b57905f139ce5299f6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803285"
---
# <a name="tokenfields"></a>!tokenfields


**！ Tokenfields** 扩展显示 (令牌结构) 的访问令牌对象中的字段的名称和偏移量。

```dbgcmd
!tokenfields
```

## <span id="ddk__tokenfields_dbg"></span><span id="DDK__TOKENFIELDS_DBG"></span>


### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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
<td align="left"><p> (，请参阅 "备注" 部分) </p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关令牌结构的信息，请参阅 Russinovich 和 David 所罗门群岛中的 *Microsoft Windows 内部机制*。 本书在某些语言和国家/地区可能不可用。 (Microsoft Windows SDK 文档中所述的用户模式令牌结构略有不同。 ) 

<a name="remarks"></a>备注
-------

此扩展命令在 Windows XP 或更高版本的 Windows 中不可用。 请改用 [**dt (显示类型)**](dt--display-type-.md) 命令，直接显示标记结构：

```dbgcmd
kd> dt nt!_TOKEN 
```

若要查看令牌结构的特定实例，请使用 [**！令牌**](-token.md) 扩展。

下面是 Windows 2000 系统中 **！ tokenfields** 的示例：

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

 

 





