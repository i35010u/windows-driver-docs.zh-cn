---
title: 远程服务器语法
description: 若要启动远程工具的服务器端，请在命令行中使用以下语法。
keywords:
- 远程服务器语法 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Remote Server Syntax
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0a176d1a44c9f77a51c3eb4e5cfe506a3e3cd560
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791979"
---
# <a name="remote-server-syntax"></a>远程服务器语法


若要启动远程工具的服务器端，请在命令行中使用以下语法。

```console
remote /s Command SessionName [/f Color] [/b] [/u User [/u User...]] [/ud User [/ud User...]] [/v | /-v]
```

## <a name="span-idddk_remote_server_syntax_dtoolsspanspan-idddk_remote_server_syntax_dtoolsspanparameters"></a><span id="ddk_remote_server_syntax_dtools"></span><span id="DDK_REMOTE_SERVER_SYNTAX_DTOOLS"></span>参数


<span id="________s______"></span><span id="________S______"></span>**/s**   
启动服务器会话。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span>*命令*   
指定启动基于控制台的程序的命令。 此命令可以包含参数。 如果命令包括空格，请将其括在引号中。

<span id="_______SessionName______"></span><span id="_______sessionname______"></span><span id="_______SESSIONNAME______"></span>*SessionName*   
为远程会话分配一个名称。 如果名称包含空格，请将其用引号括起来。 此参数不区分大小写。

<span id="________f______"></span><span id="________F______"></span>**/f**   
指定服务器命令窗口中文本的颜色。

<span id="________b______"></span><span id="________B______"></span>**/b**   
指定服务器命令窗口的背景色。

<span id="_______Color______"></span><span id="_______color______"></span><span id="_______COLOR______"></span>*颜色*   
指定颜色。 有效值为黑色、蓝色、绿色、青色、红色、紫色、黄色、白色、lblack、lblue、lgreen、lred、lpurple、lyellow 和 lwhite。

<span id="________u______"></span><span id="________U______"></span>**/u**   
指定允许连接到远程会话的用户或组;默认情况下，每个人都是允许的。 使用此参数时，除了 *用户* 子参数指定的用户和组外，每个人都将被拒绝。

<span id="________ud______"></span><span id="________UD______"></span>**/ud**   
指定被拒绝连接到远程会话的权限的用户或组;默认情况下，没有被拒绝的权限。

<span id="_______User______"></span><span id="_______user______"></span><span id="_______USER______"></span>*用户*   
指定用户或组的名称，其格式为 " \[ *域*  |  *计算机* \] \\ {*用户*  |  *组*}"。 指定本地计算机上的用户或组时，请省略计算机名。

<span id="________v______"></span><span id="________V______"></span>**/v**   
使会话可见。 有关详细信息，请参阅 [Visible 会话](remote-tool-concepts.md#visible-session)。

默认情况下，只有调试器会话可见，即 *Command* 参数的值包括 **kd**、 **dbg**、 **remoteds**、 **ntsd** 或 **cdb** 的会话;否则，会话将不可见。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
使远程调试器会话不可见。 有关详细信息，请参阅 [Visible 会话](remote-tool-concepts.md#visible-session)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

*Command* 和 *SessionName* 参数必须按语法行中显示的顺序出现。

若要结束远程会话，请键入 <strong>@k</strong> 。 有关详细信息，请参阅 [远程会话命令](remote-session-commands.md)。

远程工具不会创建当前用户没有加入权限的会话。

当在一台计算机上启动多个远程会话时，为每个会话打开一个新的命令窗口。 同时，为每个会话使用不同的会话名称。 由于会话名称用于标记命名管道，因此它们在计算机上必须唯一。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```console
remote /s "i386kd -v" TestSession
remote /s "cmd" "My Remote Session" /f white /b black /u Server01\Administrators
remote /s "ntsd -d -g -x" DebugIt /-v
remote /q Server01
```

 

 





