---
title: sd
description: Sd 扩展显示指定地址处的安全描述符。
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
ms.openlocfilehash: f08a439af20884b603b82f63db66a503b7b0900e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837571"
---
# <a name="sd"></a>!sd


**！ Sd** extension 显示指定地址处的安全描述符。

语法

```dbgcmd
!sd Address [Flags] 
```

## <a name="span-idddk__sd_dbgspanspan-idddk__sd_dbgspanparameters"></a><span id="ddk__sd_dbg"></span><span id="DDK__SD_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定安全描述符结构的十六进制地址 \_ 。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
如果此设置为1，则显示友好名称。 这包括 sid) 类型 (安全标识符，以及 SID 的域和用户名。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Exts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

对于应用程序和此命令的示例，请参阅 [确定对象的 ACL](determining-the-acl-of-an-object.md)。 有关安全描述符的详细信息，请参阅 Microsoft Windows SDK 文档、Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，并标记 Russinovich 和 David 所罗门群岛。 另请参阅 [**！ sid**](-sid.md) 和 [**！ acl**](-acl.md)。

<a name="remarks"></a>备注
-------

以下是示例：

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

 

 





