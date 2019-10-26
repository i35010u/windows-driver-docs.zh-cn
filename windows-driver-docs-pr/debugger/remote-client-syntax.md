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
ms.openlocfilehash: 2ad54a20220119253cfcf3c894eac2a03409473d
ms.sourcegitcommit: d2dab8b8bf335835d0341ca3f0a36eab0ec028f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72892686"
---
# <a name="remote-client-syntax"></a>远程客户端语法
若要启动远程工具的客户端，请在命令行中使用以下语法。

```console
remote /c Server SessionName [/L Lines] [/f] [/b] [/k ColorFile] 
```

## <a name="span-idparametersspanspan-idparametersspanparameters"></a><span id="parameters"></span><span id="PARAMETERS"></span>Parameters

<span id="________c______"></span><span id="________C______"></span> **/c**   
将客户端连接到远程会话。

<span id="_______Server______"></span><span id="_______server______"></span><span id="_______SERVER______"></span>*服务器*   
指定建立会话的服务器的计算机名称。

<span id="_______SessionName______"></span><span id="_______sessionname______"></span><span id="_______SESSIONNAME______"></span>*SessionName*   
指定远程会话的名称。 此参数不区分大小写。

<span id="________L_______Lines______"></span><span id="________l_______lines______"></span><span id="________L_______LINES______"></span> **/L** *行*   
指定发送到客户端计算机的控制台显示的行数。 默认值为200行。 *线条*是一个十进制数。

<span id="________f______"></span><span id="________F______"></span> **/f**   
指定服务器命令窗口中文本的颜色。

<span id="________b______"></span><span id="________B______"></span> **/b**   
指定服务器命令窗口的背景色。

<span id="_______Color______"></span><span id="_______color______"></span><span id="_______COLOR______"></span>*颜色*   
指定颜色。 有效值为黑色、蓝色、绿色、青色、红色、紫色、黄色、白色、lblack、lblue、lgreen、lred、lpurple、lyellow 和 lwhite。

<span id="________k_______ColorFile______"></span><span id="________k_______colorfile______"></span><span id="________K_______COLORFILE______"></span> **/K** *ColorFile*   
指示格式化文本文件的路径（可选）和名称，该文件指定用于在客户端计算机上显示输出的颜色。

颜色文件将输出中的关键字与文本颜色关联起来。 当关键字出现在输出行中时，远程工具会将关联的文本颜色应用到该行。 有关文件的格式，请参阅 "备注"。

<span id="________q_______Computer______"></span><span id="________q_______computer______"></span><span id="________Q_______COMPUTER______"></span> **/Q** *计算机*   
显示在指定计算机上可用的远程会话。 列表中只显示可见会话。 （请参阅[**远程服务器语法**](remote-server-syntax.md)中的 **/v** 。）

## <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

*服务器*和*SessionName*参数必须按语法行中显示的顺序出现。

若要断开与远程会话的连接，请键入<strong>@q</strong>。 有关详细信息，请参阅[远程会话命令](remote-session-commands.md)。

**关键字颜色文件。** 关键字颜色文件的格式如下所示。 关键字解释器不区分大小写。

关键字或短语单独显示在一行上。 与关键字关联的颜色会自行出现在以下行中，如以下语法中所示：

```text
Keyword
TextColor[, BackgroundColor]
```

例如，以下文件指示 Remote 在浅红色背景上以黑色文本显示包含单词 "error" 的行;如果为，则以浅蓝色显示包含 "warning" 一词的行，在默认背景下显示包含短语 "Windows Vista" 的行。

```text
ERROR
black, lred
WARNING
lblue
Windows Vista
lgreen
```

## <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```console
remote /c Server01 TestSession
remote /c Domain1\ComputerA0 "cmd" "My Remote Session"
remote /c Server01 TestSession /L 50 /f black /b white /k c:\remote_file.txt
remote /q Server01
```
