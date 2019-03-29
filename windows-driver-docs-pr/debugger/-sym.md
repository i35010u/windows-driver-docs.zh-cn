---
title: 符号
description: 符号扩展控件干扰符号加载和符号提示。
ms.assetid: 84551b24-740c-4289-acc4-8a0053f80b41
keywords:
- 符号，干扰符号加载
- 符号提示
- Windows 调试的符号
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sym
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8d83a66e563f5e3022f311c93d06593d51d929d2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562978"
---
# <a name="sym"></a>!sym


**！ 符号**干扰性的扩展控件符号加载和符号提示。

```dbgcmd
!sym 
!sym noisy 
!sym quiet 
!sym prompts 
!sym prompts off
```

## <a name="span-idddksymdbgspanspan-idddksymdbgspanparameters"></a><span id="ddk__sym_dbg"></span><span id="DDK__SYM_DBG"></span>参数


<span id="_______noisy______"></span><span id="_______NOISY______"></span> **noisy**   
激活干扰符号加载。

<span id="_______quiet______"></span><span id="_______QUIET______"></span> **quiet**   
停用干扰符号加载。

<span id="_______prompts______"></span><span id="_______PROMPTS______"></span> **prompts**   
允许身份验证对话框 SymSrv 收到身份验证请求时出现。

<span id="_______prompts_off______"></span><span id="_______PROMPTS_OFF______"></span> **关闭的提示**   
SymSrv 收到身份验证请求时，禁止显示所有身份验证对话框。 这可能会导致 SymSrv 正在访问符号无法通过 internet。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Dbghelp.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果 **！ 符号**扩展不带任何参数，则显示干扰符号加载和符号提示的当前状态。

**！ 符号干扰**并 **！ 符号静默**扩展控制干扰符号加载。 有关详细信息以及显示和更改此选项的其他方法，请参阅[SYMOPT\_调试](symbol-options.md#symopt-debug)。

**！ 符号提示**并 **！ 符号提示关闭**扩展控制 SymSrv 遇到身份验证请求时是否显示身份验证对话框。 这些命令的后面必须跟[ **.reload （重新加载模块）** ](-reload--reload-module-.md)它们才会生效。 可通过代理服务器，internet 防火墙、 智能卡读卡器和安全网站发送身份验证请求。 有关详细信息和更改此选项的其他方法，请参阅[防火墙和代理服务器](firewalls-and-proxy-servers.md)。

**请注意**  干扰符号加载不应混淆干扰源加载-由控制[ **（干扰源加载） 可通过.srcnoisy** ](-srcnoisy--noisy-source-loading-.md)命令。

 

 

 





