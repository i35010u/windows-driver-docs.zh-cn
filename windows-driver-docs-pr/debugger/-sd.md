---
title: sd
description: Sd 扩展显示指定地址处的安全描述符。
ms.assetid: 67c72bdb-7bfc-42d6-9b65-31a07dc67729
keywords:
- sd Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sd
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e6a19fabf60c052308b7e5b3d8254143339615c9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334232"
---
# <a name="sd"></a>!sd


**！ Sd**扩展显示指定地址处的安全描述符。

语法

```dbgcmd
!sd Address [Flags] 
```

## <a name="span-idddksddbgspanspan-idddksddbgspanparameters"></a><span id="ddk__sd_dbg"></span><span id="DDK__SD_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定安全的十六进制地址\_描述符结构。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
如果此值设置为 1，显示的友好名称。 这包括安全标识符 (SID) 类型，以及域和用户名称的 sid。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Exts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

应用程序和此命令的示例，请参阅[确定对象的 ACL](determining-the-acl-of-an-object.md)。 有关安全描述符信息，请参阅 Microsoft Windows SDK 文档，Windows Driver Kit (WDK) 文档，并*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 另请参阅[ **！ sid** ](-sid.md)并[ **！ acl**](-acl.md)。

<a name="remarks"></a>备注
-------

下面是一个示例：

```dbgcmd
kd> !sd e1a96a80 1
->Revision: 0x1
->Sbz1    : 0x0
->Control : 0x8004
            SE_DACL_PRESENT
            SE_SELF_RELATIVE
->Owner   : S-1-5-21-518066528-515770016-299552555-2981724 (User: MYDOMAIN\myuser)
->Group   : S-1-5-21-518066528-515770016-299552555-513 (Group: MYDOMAIN\Domain Users)
->Dacl    :
->Dacl    : ->AclRevision: 0x2
->Dacl    : ->Sbz1       : 0x0
->Dacl    : ->AclSize    : 0x40
->Dacl    : ->AceCount   : 0x2
->Dacl    : ->Sbz2       : 0x0
->Dacl    : ->Ace[0]: ->AceType: ACCESS_ALLOWED_ACE_TYPE
->Dacl    : ->Ace[0]: ->AceFlags: 0x0
->Dacl    : ->Ace[0]: ->AceSize: 0x24
->Dacl    : ->Ace[0]: ->Mask : 0x001f0003
->Dacl    : ->Ace[0]: ->SID: S-1-5-21-518066528-515770016-299552555-2981724 (User: MYDOMAIN\myuser)

->Dacl    : ->Ace[1]: ->AceType: ACCESS_ALLOWED_ACE_TYPE
->Dacl    : ->Ace[1]: ->AceFlags: 0x0
->Dacl    : ->Ace[1]: ->AceSize: 0x14
->Dacl    : ->Ace[1]: ->Mask : 0x001f0003
->Dacl    : ->Ace[1]: ->SID: S-1-5-18 (Well Known Group: NT AUTHORITY\SYSTEM)

->Sacl    :  is NULL
```

 

 





