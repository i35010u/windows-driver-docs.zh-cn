---
title: 确定对象的 ACL
description: 确定对象的 ACL
ms.assetid: 8dcd4f5a-1415-4a58-bfb1-fd3cbd58cc56
keywords:
- 访问控制列表 (ACL)
- ACL （访问控制列表）
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e43c405d40b0768ac348dc0aeed0be372a5529b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346307"
---
# <a name="determining-the-acl-of-an-object"></a>确定对象的 ACL


## <span id="ddk_determining_the_acl_of_an_object_dbg"></span><span id="DDK_DETERMINING_THE_ACL_OF_AN_OBJECT_DBG"></span>


可以使用调试器来检查对象的访问控制列表 (ACL)。

如果您正在执行内核调试，可以使用以下方法。 若要使用它执行用户模式下调试时，需要将控件重定向到内核调试程序。 请参阅[控制用户模式下调试程序与内核调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md)有关详细信息。

首先，使用[ **！ 对象**](-object.md)调试器扩展与相关对象的名称：

```dbgcmd
kd> !object \BaseNamedObjects\AgentToWkssvcEvent
Object: ffbb8a98  Type: (80e30e70) Event
    ObjectHeader: ffbb8a80
    HandleCount: 2  PointerCount: 3
    Directory Object: e14824a0  Name: AgentToWkssvcEvent
```

这将显示对象标头具有地址 0xFFBB8A80。 使用[ **dt （显示类型）** ](dt--display-type-.md)命令使用此地址和**nt ！\_对象\_标头**结构名称：

```dbgcmd
kd> dt nt!_OBJECT_HEADER ffbb8a80
   +0x000 PointerCount     : 3
   +0x004 HandleCount      : 2
   +0x004 NextToFree       : 0x00000002
 +0x008 Type             : 0x80e30e70
   +0x00c NameInfoOffset   : 0x10 '
 +0x00d HandleInfoOffset : 0 '
   +0x00e QuotaInfoOffset  : 0 '
   +0x00f Flags            : 0x20 ' '
   +0x010 ObjectCreateInfo : 0x8016b460
   +0x010 QuotaBlockCharged : 0x8016b460
   +0x014 SecurityDescriptor : 0xe11f08b6
   +0x018 Body             : _QUAD
```

安全描述符指针值显示为 0xE11F08B6。 此值最低的 3 位表示过去的此结构的开头的偏移量，因此应忽略它们。 换而言之，安全\_描述符结构实际上开始 0xE11F08B6 & ~ 0x7。 使用[ **！ sd** ](-sd.md)此地址上的扩展：

```dbgcmd
kd> !sd e11f08b0
->Revision: 0x1
->Sbz1    : 0x0
->Control : 0x8004
            SE_DACL_PRESENT
 SE_SELF_RELATIVE
->Owner   : S-1-5-32-544
->Group   : S-1-5-18
->Dacl    : 
->Dacl    : ->AclRevision: 0x2
->Dacl    : ->Sbz1       : 0x0
->Dacl    : ->AclSize    : 0x44
->Dacl    : ->AceCount   : 0x2
->Dacl    : ->Sbz2       : 0x0
->Dacl    : ->Ace[0]: ->AceType: ACCESS_ALLOWED_ACE_TYPE
->Dacl    : ->Ace[0]: ->AceFlags: 0x0
->Dacl    : ->Ace[0]: ->AceSize: 0x14
->Dacl    : ->Ace[0]: ->Mask : 0x001f0003
->Dacl    : ->Ace[0]: ->SID: S-1-5-18

->Dacl    : ->Ace[1]: ->AceType: ACCESS_ALLOWED_ACE_TYPE
->Dacl    : ->Ace[1]: ->AceFlags: 0x0
->Dacl    : ->Ace[1]: ->AceSize: 0x18
->Dacl    : ->Ace[1]: ->Mask : 0x00120001
->Dacl    : ->Ace[1]: ->SID: S-1-5-32-544

->Sacl    :  is NULL
```

这将显示此对象的安全信息。

 

 





