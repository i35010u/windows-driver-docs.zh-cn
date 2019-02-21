---
title: acl
description: Acl 扩展设置格式并显示内容的访问控制列表 (ACL)。
ms.assetid: 591f56b6-5a70-4037-a285-a1bffd5bd387
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
ms.openlocfilehash: d54dc14c65e72cd0ca43b4536305ea354bedc0f9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519706"
---
# <a name="acl"></a>！ acl


**！ Acl**扩展设置格式并显示内容的访问控制列表 (ACL)。

语法

```dbgcmd
    !acl Address [Flags] 
```

## <a name="span-idddkacldbgspanspan-idddkacldbgspanparameters"></a><span id="ddk__acl_dbg"></span><span id="DDK__ACL_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定 ACL 的十六进制地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
如果显示的 ACL，友好名称的值*标志*为 1。 此友好名称，包括安全标识符 (SID) 类型和 SID 的域和用户名称。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Exts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

关于访问控制列表的详细信息，请参阅[ **！ sid**](-sid.md)， [ **！ sd**](-sd.md)，和[确定对象的 ACL](determining-the-acl-of-an-object.md). 此外，请参阅 Microsoft Windows SDK 文档，Windows Driver Kit (WDK) 文档，并*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。

<a name="remarks"></a>备注
-------

下面的示例演示 **！ acl**扩展。

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

 

 





