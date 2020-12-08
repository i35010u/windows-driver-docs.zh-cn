---
title: 会话
description: 会话扩展控制会话上下文。 它还可以显示所有用户会话的列表。
keywords:
- 会话 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- session
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d88f91439b574dbb31226cd707fa39bbabdeeca0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802077"
---
# <a name="session"></a>!session


**！会话** 扩展控制会话上下文。 它还可以显示所有用户会话的列表。

语法

```dbgcmd
!session 
!session -s DefaultSession 
!session -?
```

## <a name="span-idddk__session_dbgspanspan-idddk__session_dbgspanparameters"></a><span id="ddk__session_dbg"></span><span id="DDK__SESSION_DBG"></span>参数


<span id="_______-s_______DefaultSession______"></span><span id="_______-s_______defaultsession______"></span><span id="_______-S_______DEFAULTSESSION______"></span>**-s**  **** *DefaultSession*   
将 [会话上下文](changing-contexts.md#session-context) 设置为指定值。 如果 *DefaultSession* 为-1，则会话上下文设置为当前会话。

<span id="_______-_______"></span> **-?**   
在调试器中显示此扩展的帮助命令窗口。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关用户会话和会话管理器 ( # A0) 的信息，请参阅 Russinovich 和 David 所罗门群岛的 *Microsoft Windows 内部机制*。

<a name="remarks"></a>备注
-------

**！会话** 扩展用于控制会话上下文。 使用不带参数的 **！会话** 将在目标计算机上显示活动会话的列表。 使用 **！ session/S** *DefaultSession* 会将会话上下文更改为新的默认值。

设置会话上下文时，进程上下文会自动更改为该会话的活动进程，并启用 [**cache forcedecodeptes**](-cache--set-cache-size-.md) 选项，以便正确转换会话地址。

有关更多详细信息以及受会话上下文影响的所有与会话相关的扩展的列表，请参阅 [更改上下文](changing-contexts.md)。

 

 





