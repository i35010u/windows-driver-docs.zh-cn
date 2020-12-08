---
title: acl
description: Acl 扩展会格式化并显示访问控制列表 (ACL) 的内容。
keywords:
- acl Windows 调试
ms.date: 09/17/2018
topic_type:
- apiref
api_name:
- acl
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 45855a1d2b59efca8e64dd36daedba4b14b33193
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800175"
---
# <a name="acl"></a>!acl


**！ Acl** 扩展格式并显示访问控制列表 (acl) 的内容。

语法

```dbgcmd
    !acl Address [Flags] 
```

## <a name="span-idddk__acl_dbgspanspan-idddk__acl_dbgspanparameters"></a><span id="ddk__acl_dbg"></span><span id="DDK__ACL_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 ACL 的十六进制地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
如果 *Flags* 的值为1，则显示 ACL 的友好名称。 此友好名称包括 sid) 类型的安全 (标识符，以及 SID 的域和用户名。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Exts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关访问控制列表的详细信息，请参阅 [**！ sid**](-sid.md)， [**！ Sd**](-sd.md)，并 [确定对象的 ACL](determining-the-acl-of-an-object.md)。 另请参阅 Microsoft Windows SDK 文档、Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

下面的示例演示 **！ acl** 扩展。

```console
kd> !acl e1bf35d4 1
ACL is:
ACL is: ->AclRevision: 0x2
ACL is: ->Sbz1       : 0x0
ACL is: ->AclSize    : 0x40
ACL is: ->AceCount   : 0x2
ACL is: ->Sbz2       : 0x0
ACL is: ->Ace[0]: ->AceType: ACCESS_ALLOWED_ACE_TYPE
ACL is: ->Ace[0]: ->AceFlags: 0x0
ACL is: ->Ace[0]: ->AceSize: 0x24
ACL is: ->Ace[0]: ->Mask : 0x10000000
ACL is: ->Ace[0]: ->SID: S-1-5-21-518066528-515770016-299552555-2981724 (User: MYDOMAIN\myuser)

ACL is: ->Ace[1]: ->AceType: ACCESS_ALLOWED_ACE_TYPE
ACL is: ->Ace[1]: ->AceFlags: 0x0
ACL is: ->Ace[1]: ->AceSize: 0x14
ACL is: ->Ace[1]: ->Mask : 0x10000000
ACL is: ->Ace[1]: ->SID: S-1-5-18 (Well Known Group: NT AUTHORITY\SYSTEM)
```

 

 





