---
title: 远程服务器语法
description: 若要启动远程工具的服务器端，请在命令行中使用以下语法。
ms.assetid: fecc9f43-6946-4d99-840b-a85c75ac397c
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
ms.openlocfilehash: 93fa605ad436efbf676756cdd871888f1c198045
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353504"
---
# <a name="remote-server-syntax"></a>远程服务器语法


若要启动远程工具的服务器端，请在命令行中使用以下语法。

```console
remote /s Command SessionName [/f Color] [/b] [/u User [/u User...]] [/ud User [/ud User...]] [/v | /-v]
```

## <a name="span-idddkremoteserversyntaxdtoolsspanspan-idddkremoteserversyntaxdtoolsspanparameters"></a><span id="ddk_remote_server_syntax_dtools"></span><span id="DDK_REMOTE_SERVER_SYNTAX_DTOOLS"></span>参数


<span id="________s______"></span><span id="________S______"></span> **/s**   
启动服务器会话。

<span id="_______Command______"></span><span id="_______command______"></span><span id="_______COMMAND______"></span> *命令*   
指定启动基于控制台的程序的命令。 此命令可以包含参数。 如果该命令包含空格，则将其括在引号中。

<span id="_______SessionName______"></span><span id="_______sessionname______"></span><span id="_______SESSIONNAME______"></span> *SessionName*   
将名称分配到远程会话。 如果名称包含空格，请将其括在引号中。 此参数不区分大小写。

<span id="________f______"></span><span id="________F______"></span> **/f**   
在服务器命令窗口中指定的文本颜色。

<span id="________b______"></span><span id="________B______"></span> **/b**   
指定服务器命令窗口的背景色。

<span id="_______Color______"></span><span id="_______color______"></span><span id="_______COLOR______"></span> *颜色*   
指定一种颜色。 有效的值为黑色、 蓝色、 绿色、 蓝绿色、 红色、 紫色、 黄色、 白色、 lblack、 lblue、 lgreen、 lred、 lpurple、 lyellow 和 lwhite。

<span id="________u______"></span><span id="________U______"></span> **/u**   
指定用户或组有权连接到远程会话;默认情况下，允许任何人。 如果使用此参数，每个人都被拒绝权限的用户和组指定的除外*用户*子参数。

<span id="________ud______"></span><span id="________UD______"></span> **/ud**   
指定用户或组会遭到拒绝连接到远程会话; 的权限默认情况下，没有人拒绝的权限。

<span id="_______User______"></span><span id="_______user______"></span><span id="_______USER______"></span> *用户*   
指定用户或组中的名称\[*域* | *计算机*\]\\{*用户* | *组*} 格式。 在本地计算机上指定的用户或组，则省略计算机名称。

<span id="________v______"></span><span id="________V______"></span> **/v**   
使会话可见。 有关详细信息，请参阅[可见会话](remote-tool-concepts.md#visible-session)。

默认情况下，仅调试器会话是可见的也就是说，在其中的会话的值*命令*参数包含词**kd**， **dbg**， **remoteds**， **ntsd**，或**cdb**; 否则为该会话将不可见。

<span id="_______-v______"></span><span id="_______-V______"></span> **-v**   
使远程调试器会话不可见。 有关详细信息，请参阅[可见会话](remote-tool-concepts.md#visible-session)。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

*命令*并*SessionName*参数必须出现在语法行上显示的顺序。

若要结束远程会话，请键入<strong>@k</strong>。 有关详细信息，请参阅[会话的远程命令](remote-session-commands.md)。

远程工具不会创建当前用户无权加入的会话。

当一台计算机上启动多个远程会话，为每个会话中打开新的命令窗口。 此外，使用每个会话的不同的会话名称。 会话名称用于标记命名的管道，因为它们必须是唯一的计算机上。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```console
remote /s "i386kd -v" TestSession
remote /s "cmd" "My Remote Session" /f white /b black /u Server01\Administrators
remote /s "ntsd -d -g -x" DebugIt /-v
remote /q Server01
```

 

 





