---
title: sid
description: Sid 扩展显示指定地址处的安全标识符 (SID)。
ms.assetid: 7b93eb0e-7c0f-4c30-851b-6f40c7df8e1b
keywords:
- sid Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9c1e5a1d1afd2814d5b04962a57259af2ebcbac9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338812"
---
# <a name="sid"></a>!sid


**！ Sid**扩展显示指定地址处的安全标识符 (SID)。

语法

```dbgcmd
!sid Address [Flags] 
```

## <a name="span-idddksiddbgspanspan-idddksiddbgspanparameters"></a><span id="ddk__sid_dbg"></span><span id="DDK__SID_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
指定的 SID 结构的地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
如果此值设置为 1，显示 SID 的 SID 类型、 域和用户名称。

如果此值设置为 1，显示的友好名称。 这包括为 SID 的域和用户名称或 SID 类型。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Exts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关 Sid 的信息，请参阅 Microsoft Windows SDK 文档，Windows Driver Kit (WDK) 文档中，或*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 另请参阅[ **！ sd** ](-sd.md)并[ **！ acl**](-acl.md)。

<a name="remarks"></a>备注
-------

下面是两个示例，一个不包含所示，友好名称，另一个使用：

```dbgcmd
kd> !sid 0xe1bf35b8
SID is: S-1-5-21-518066528-515770016-299552555-513

kd> !sid 0xe1bf35b8 1
SID is: S-1-5-21-518066528-515770016-299552555-513 (Group: MYGROUP\Domain Users)
```

 

 





