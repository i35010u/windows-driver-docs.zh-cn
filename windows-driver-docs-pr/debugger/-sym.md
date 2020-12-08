---
title: 符号
description: 符号扩展控制干扰符号加载和符号提示。
keywords:
- 符号，干扰符号加载
- 符号，提示
- 符号 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- sym
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 85b94c0300e36e0090e6d3df51f72c07f24bc9df
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832035"
---
# <a name="sym"></a>!sym


**！符号** extension 控制干扰符号加载和符号提示。

```dbgcmd
!sym 
!sym noisy 
!sym quiet 
!sym prompts 
!sym prompts off
```

## <a name="span-idddk__sym_dbgspanspan-idddk__sym_dbgspanparameters"></a><span id="ddk__sym_dbg"></span><span id="DDK__SYM_DBG"></span>参数


<span id="_______noisy______"></span><span id="_______NOISY______"></span>**噪音**   
激活干扰符号加载。

<span id="_______quiet______"></span><span id="_______QUIET______"></span>**quiet**   
停用干扰符号加载。

<span id="_______prompts______"></span><span id="_______PROMPTS______"></span>**提示**   
允许在 SymSrv 接收到身份验证请求时显示身份验证对话框。

<span id="_______prompts_off______"></span><span id="_______PROMPTS_OFF______"></span>**提示关闭**   
当 SymSrv 接收到身份验证请求时，禁止显示所有身份验证对话框。 这可能会导致 SymSrv 无法通过 internet 访问符号。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

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

如果 **！符号** 扩展名与 no 参数一起使用，则显示当前的干扰符号加载和符号提示的状态。

**！符号干扰** 和 **！符号 quiet** extension 控制干扰符号加载。 有关详细信息和显示和更改此选项的其他方法，请参阅 [SYMOPT \_ 调试](symbol-options.md#symopt-debug)。

当 SymSrv 遇到身份验证请求时， **！符号提示** 和 **！符号会提示关闭** 扩展控制是否显示身份验证对话框。 这些命令后面必须有 [**。请重新加载 (重载模块)**](-reload--reload-module-.md) 使其生效。 代理服务器、internet 防火墙、智能卡读取器和安全网站可能会发送身份验证请求。 有关详细信息和其他更改此选项的方法，请参阅 [防火墙和代理服务器](firewalls-and-proxy-servers.md)。

**注意**   不应将干扰符号加载与干扰源加载相混淆--由 [**srcnoisy (干扰源加载)**](-srcnoisy--noisy-source-loading-.md) 命令。

 

 

 





