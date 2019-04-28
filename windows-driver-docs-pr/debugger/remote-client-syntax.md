---
title: 远程客户端语法
description: 若要启动远程工具的客户端，请在命令行中使用以下语法。
ms.assetid: 4728ef17-a365-4024-815c-2719b51b81f6
keywords:
- 远程客户端语法 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- Remote Client Syntax
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9779e7350a34fc4ced0b9750649d9acceb22b792
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353577"
---
# <a name="remote-client-syntax"></a>远程客户端语法


若要启动远程工具的客户端，请在命令行中使用以下语法。

```console
remote /c Server SessionName [/L Lines] [/f] [/b] [/k ColorFile] 
```

## <a name="span-idddkremoteclientsyntaxdtoolsspanspan-idddkremoteclientsyntaxdtoolsspanparameters"></a><span id="ddk_remote_client_syntax_dtools"></span><span id="DDK_REMOTE_CLIENT_SYNTAX_DTOOLS"></span>参数


<span id="________c______"></span><span id="________C______"></span> **/c**   
将客户端连接到远程会话。

<span id="_______Server______"></span><span id="_______server______"></span><span id="_______SERVER______"></span> *Server*   
指定的服务器建立会话的计算机名称。

<span id="_______SessionName______"></span><span id="_______sessionname______"></span><span id="_______SESSIONNAME______"></span> *SessionName*   
指定远程会话的名称。 此参数不区分大小写。

<span id="________L_______Lines______"></span><span id="________l_______lines______"></span><span id="________L_______LINES______"></span> **/L** *行*   
指定发送到客户端计算机从控制台中显示的行数。 默认值为 200 行。 *行*是一个十进制数。

<span id="________f______"></span><span id="________F______"></span> **/f**   
在服务器命令窗口中指定的文本颜色。

<span id="________b______"></span><span id="________B______"></span> **/b**   
指定服务器命令窗口的背景色。

<span id="_______Color______"></span><span id="_______color______"></span><span id="_______COLOR______"></span> *颜色*   
指定一种颜色。 有效的值为黑色、 蓝色、 绿色、 蓝绿色、 红色、 紫色、 黄色、 白色、 lblack、 lblue、 lgreen、 lred、 lpurple、 lyellow 和 lwhite。

<span id="________k_______ColorFile______"></span><span id="________k_______colorfile______"></span><span id="________K_______COLORFILE______"></span> **/k** *ColorFile*   
指示路径 （可选） 和指定颜色的客户端计算机上显示输出的格式化的文本文件的名称。

颜色文件将在输出中的关键字与文本的颜色相关联。 当关键字出现在输出的行时，远程工具将应用到该行的关联的文本颜色。 文件的格式，请参阅"备注"。

<span id="________q_______Computer______"></span><span id="________q_______computer______"></span><span id="________Q_______COMPUTER______"></span> **/q** *Computer*   
显示指定计算机上可用的远程会话。 仅显示会话出现在列表中。 (请参阅 **/v**中[**远程服务器语法**](remote-server-syntax.md)。)

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

*服务器*并*SessionName*参数必须出现在语法行上显示的顺序。

若要从远程会话断开连接，请键入<strong>@q</strong>。 有关详细信息，请参阅[会话的远程命令](remote-session-commands.md)。

**关键字颜色文件。** 关键字颜色文件的格式如下所示。 关键字解释器不区分大小写。

关键字或短语将显示在行本身。 与该关键字关联的颜色单独显示在下一行，如语法中所示：

```text
Keyword
TextColor[, BackgroundColor]
```

例如，以下文件指示远程显示浅红色背景; 上的黑色文本中包含单词"error"的行若要显示的浅蓝色 （默认背景） 和包含短语"Windows Vista"淡绿色默认背景上的行中的行包含词"警告"。

```text
ERROR
black, lred
WARNING
lblue
Windows Vista
lgreen
```

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```console
remote /c Server01 TestSession
remote /c Domain1\ComputerA0 "cmd" "My Remote Session"
remote /c Server01 TestSession /L 50 /f black /b white /k c:\remote_file.txt
remote /q Server01
```

 

 





