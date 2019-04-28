---
title: .quit_lock（防止意外退出）
description: .Quit_lock 命令设置密码，以防用户意外结束调试会话。
ms.assetid: fd40e642-beba-4da0-a072-6493588980de
keywords:
- .quit_lock （防止意外退出） Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .quit_lock (Prevent Accidental Quit)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: a3c975a14ce2adfeabd2604b35c06d1bbb92b629
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335757"
---
# <a name="quitlock-prevent-accidental-quit"></a>.quit\_锁 （防止意外后退出）


**.Quit\_锁**命令将设置密码，以防用户意外结束调试会话。

```dbgcmd
.quit_lock /s NewPassword 
.quit_lock /q Password 
.quit_lock 
```

## <a name="span-idddkmetapreventaccidentalquitdbgspanspan-idddkmetapreventaccidentalquitdbgspanparameters"></a><span id="ddk_meta_prevent_accidental_quit_dbg"></span><span id="DDK_META_PREVENT_ACCIDENTAL_QUIT_DBG"></span>参数


<span id="________s_NewPassword_____________"></span><span id="________s_newpassword_____________"></span><span id="________S_NEWPASSWORD_____________"></span> **/s** **** *NewPassword*   
阻止调试会话结束，并将存储*NewPassword*。 无法结束直到您使用的调试器会话 **.quit\_锁定 /q**命令及此相同的密码。 *NewPassword*可以是任意字符串。 如果它包含空格，必须将*NewPassword*引号引起来。

<span id="________q_Password______________"></span><span id="________q_password______________"></span><span id="________Q_PASSWORD______________"></span> **/q** **** *Password*   
启用调试会话结束。 *密码*必须与设置的密码相匹配 **.quit\_锁定 /s**命令。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>模式</strong></p></td>
<td align="left"><p>用户模式下，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时、 崩溃转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

不带参数， **.quit\_锁**显示当前的锁状态，包括密码的完整文本。

可以重复 **.quit\_锁定 /s**命令以更改现有密码。

当你使用 **.quit\_锁定 /q**，删除该锁。 此命令不会关闭调试器。 相反，命令将仅，您可以根据需要按一般方式退出会话。

**请注意**  密码不是"机密"。 附加到调试会话的远程用户可以使用 **.quit\_锁**来确定密码。 此命令的目的是防止意外使用[ **q (Quit)** ](q--qq--quit-.md)命令。 此命令是在重新启动调试会话可能会很困难 （例如，远程在调试期间） 特别有用。

 

不能使用 **.quit\_锁定 /s**命令，在[安全模式下](activating-secure-mode.md)。 如果安全模式下才使用此命令激活，保留密码保护，但不能更改或删除密码。

 

 





