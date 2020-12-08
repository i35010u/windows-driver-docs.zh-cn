---
title: wmitrace. searchpath
description: Wmitrace. searchpath 扩展为跟踪缓冲区中的消息指定跟踪消息格式文件的位置。
keywords:
- wmitrace searchpath Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.searchpath
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7eb9b2a29b6fa8a68c6322ee7eb35ab11b267ebf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837357"
---
# <a name="wmitracesearchpath"></a>!wmitrace.searchpath


**！ Wmitrace. searchpath** 扩展为跟踪缓冲区中的消息指定跟踪消息格式文件的位置。

```dbgcmd
!wmitrace.searchpath [+] TMFPath 
!wmitrace.searchpath
```

## <a name="span-idddk__wmitrace_searchpath_dbgspanspan-idddk__wmitrace_searchpath_dbgspanparameters"></a><span id="ddk__wmitrace_searchpath_dbg"></span><span id="DDK__WMITRACE_SEARCHPATH_DBG"></span>参数


<span id="______________"></span> **+**   
导致 *TMFPath* 追加到现有搜索路径。 如果未使用 plus (+) 标记， *TMFPath* 将替换现有的搜索路径。

<span id="_______TMFPath______"></span><span id="_______tmfpath______"></span><span id="_______TMFPATH______"></span>*TMFPath*   
调试器应在其中查找跟踪消息格式文件的目录的路径。 不支持包含空格的路径。 如果包含多个路径，它们应该用分号分隔，整个字符串应用引号引起来。 如果路径用引号引起来，则反斜杠字符前面必须加上转义符 ( `"c:\\debuggers;c:\\debuggers2"` ) 。 **+** 使用令牌时， *TMFPath* 将追加到现有路径，在现有路径和新路径之间自动插入分号; 但是，如果使用了该 **+** 令牌，则无法使用引号。

<span id="_____________"></span>   

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace.dll 导出。

此扩展在 windows 2000 和更高版本的 Windows 中可用。 如果要将此扩展与 Windows 2000 一起使用，必须先将 Wmitrace.dll 文件从 Windows 的调试工具安装目录的 winxp 子目录复制到 w2kfre 子目录。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK。 有关跟踪消息格式文件的信息，请参阅 Windows 驱动程序工具包 (WDK) 中的 "跟踪消息格式文件" 主题。

<a name="remarks"></a>备注
-------

当与没有参数一起使用时， **！ wmitrace** 显示当前搜索路径。

跟踪消息格式文件 (\*) 包含用于格式化跟踪提供程序生成的二进制跟踪消息的说明。

*TMFPath* 参数必须只包含目录的路径;它不能包含文件名。 TMF 文件的名称是消息 GUID 后跟. TMF 扩展。 当系统设置消息的格式时，它会读取消息的消息 GUID，并以递归方式搜索其名称与消息 GUID （从指定目录开始）的 TMF 文件。

Windows 需要 TMF 文件才能格式化缓冲区中的二进制跟踪消息。 使用！ **wmitrace; searchpath** 或！ [**WMITRACE**](-wmitrace-tmffile.md) 来指定 TMF 文件，然后使用 [**！ wmitrace**](-wmitrace-dynamicprint.md) [**或 dynamicprint**](-wmitrace-logdump.md) wmitrace 显示跟踪缓冲区内容。

如果不使用任何一个 **！ wmitrace** 或 [**tmffile**](-wmitrace-tmffile.md)，系统将使用跟踪 \_ 格式 \_ 搜索 \_ 路径环境变量的值。 如果该变量不存在，它将使用 Windows 中包含的 tmf 文件。 如果系统无法找到跟踪消息的任何格式设置信息，则它将写入 "找不到任何格式信息" 错误消息，而不是跟踪消息内容的位置。

 

 





