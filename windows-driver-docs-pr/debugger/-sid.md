---
title: sid
description: Sid 扩展显示指定地址 (SID) 安全标识符。
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
ms.openlocfilehash: 6a37a77a9da445248253f2157b4f2faaf134d777
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795731"
---
# <a name="sid"></a>!sid


**！ Sid** 扩展显示指定地址 (sid) 安全标识符。

语法

```dbgcmd
!sid Address [Flags] 
```

## <a name="span-idddk__sid_dbgspanspan-idddk__sid_dbgspanparameters"></a><span id="ddk__sid_dbg"></span><span id="DDK__SID_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
指定 SID 结构的地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
如果此设置为1，则显示 SID 的 SID 类型、域和用户名。

如果此设置为1，则显示友好名称。 这包括 SID 类型以及 SID 的域和用户名。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Exts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 Sid 的详细信息，请参阅 Microsoft Windows SDK 文档、Windows 驱动程序工具包 (WDK) 文档或 *Microsoft Windows 内部机制* ，并将标记 Russinovich 和 David 所罗门群岛。 另请参阅 [**！ sd**](-sd.md) 和 [**！ acl**](-acl.md)。

<a name="remarks"></a>备注
-------

下面是两个示例，一个示例没有显示友好名称，另一个用于：

```dbgcmd
kd> !sid 0xe1bf35b8
SID is: S-1-5-21-518066528-515770016-299552555-513

kd> !sid 0xe1bf35b8 1
SID is: S-1-5-21-518066528-515770016-299552555-513 (Group: MYGROUP\Domain Users)
```

 

 





