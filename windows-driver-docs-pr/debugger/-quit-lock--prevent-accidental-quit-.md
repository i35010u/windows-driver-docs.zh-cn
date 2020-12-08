---
title: .quit_lock（防止意外退出）
description: .Quit_lock 命令设置密码以防止意外终止调试会话。
keywords:
- .quit_lock (防止意外退出) Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .quit_lock (Prevent Accidental Quit)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 73044bc7859a985bcdacabdc88942cbb821db406
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821027"
---
# <a name="quit_lock-prevent-accidental-quit"></a>。退出 \_ 锁 (防止意外退出) 


**Quit \_ lock** 命令设置密码以防止意外终止调试会话。

```dbgcmd
.quit_lock /s NewPassword 
.quit_lock /q Password 
.quit_lock 
```

## <a name="span-idddk_meta_prevent_accidental_quit_dbgspanspan-idddk_meta_prevent_accidental_quit_dbgspanparameters"></a><span id="ddk_meta_prevent_accidental_quit_dbg"></span><span id="DDK_META_PREVENT_ACCIDENTAL_QUIT_DBG"></span>参数


<span id="________s_NewPassword_____________"></span><span id="________s_newpassword_____________"></span><span id="________S_NEWPASSWORD_____________"></span>**/s**  **** *NewPassword*   
阻止调试会话结束并存储 *NewPassword*。 在将 **. quit \_ lock/q** 命令与此同一密码一起使用之前，无法结束调试器会话。 *NewPassword* 可以是任意字符串。 如果包含空格，则必须用引号将 *NewPassword* 引起来。

<span id="________q_Password______________"></span><span id="________q_password______________"></span><span id="________Q_PASSWORD______________"></span>**/q**  **** *密码*   
使调试会话结束。 *密码* 必须与用 **. quit \_ lock/s** 命令设置的密码匹配。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果没有参数，则 **退出 \_ 锁** 将显示当前锁定状态，包括密码的完整文本。

可以重复使用 **quit \_ lock/s** 命令更改现有密码。

使用时，请 **退出 \_ 锁/q**。 此命令不会关闭调试器。 相反，该命令仅允许您在需要时以典型方式退出会话。

**注意**   密码不是 "机密"。 任何附加到调试会话的远程用户都可以使用 **。请退出 \_ 锁** 来确定密码。 此命令的目的是为了防止意外使用 [**q (Quit)**](q--qq--quit-.md) 命令。 如果重新启动调试会话可能很难 (例如，在远程调试) 期间，此命令特别有用。

 

不能在 [安全模式下](activating-secure-mode.md)使用 **. quit \_ lock/s** 命令。 如果在激活安全模式之前使用此命令，则密码保护将保留，但你无法更改或删除密码。

 

 





