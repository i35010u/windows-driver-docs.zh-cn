---
title: 会话
description: 会话扩展控制会话上下文。 它还可以显示所有用户会话的列表。
ms.assetid: c5f32bf0-59b5-4274-9271-1ad4913ffa1a
keywords:
- Windows 调试会话
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- session
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c51bf0bc2461d62f62e7ad2fc2a639b2e4e02eea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544838"
---
# <a name="session"></a>！ 会话


**！ 会话**扩展控制会话上下文。 它还可以显示所有用户会话的列表。

语法

```dbgcmd
!session 
!session -s DefaultSession 
!session -?
```

## <a name="span-idddksessiondbgspanspan-idddksessiondbgspanparameters"></a><span id="ddk__session_dbg"></span><span id="DDK__SESSION_DBG"></span>参数


<span id="_______-s_______DefaultSession______"></span><span id="_______-s_______defaultsession______"></span><span id="_______-S_______DEFAULTSESSION______"></span> **-s** **** *DefaultSession*   
集[会话上下文](changing-contexts.md#session-context)为指定的值。 如果*DefaultSession*为-1，上下文设置为当前会话的会话。

<span id="_______-_______"></span> **-?**   
显示此扩展在调试器命令窗口中的帮助。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关用户会话和会话管理器 (smss.exe) 的信息，请参阅*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。

<a name="remarks"></a>备注
-------

**！ 会话**使用扩展来控制会话上下文。 使用 **！ 会话**不带任何参数将显示一组活动会话的目标计算机上。 使用 **！ 会话 /s** *DefaultSession*将更改为新的默认值的会话上下文。

设置会话上下文后，进程上下文自动为该会话，更改为活动进程和[ **.cache forcedecodeptes** ](-cache--set-cache-size-.md) ，以便会话地址启用选项正确转换。

有关更多详细信息和所有受会话上下文与会话相关的扩展插件的列表，请参阅[更改上下文](changing-contexts.md)。

 

 





