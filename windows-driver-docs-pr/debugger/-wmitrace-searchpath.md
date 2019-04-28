---
title: wmitrace.searchpath
description: Wmitrace.searchpath 扩展跟踪缓冲区中指定的消息的跟踪消息格式文件的位置。
ms.assetid: 528c997c-007c-4046-92cc-169c7720b3fe
keywords:
- wmitrace.searchpath Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.searchpath
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0c55996754f97b744b3bc6595c0ce3a3c8caf301
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347237"
---
# <a name="wmitracesearchpath"></a>!wmitrace.searchpath


**！ Wmitrace.searchpath**扩展跟踪缓冲区中指定的消息的跟踪消息格式文件的位置。

```dbgcmd
!wmitrace.searchpath [+] TMFPath 
!wmitrace.searchpath
```

## <a name="span-idddkwmitracesearchpathdbgspanspan-idddkwmitracesearchpathdbgspanparameters"></a><span id="ddk__wmitrace_searchpath_dbg"></span><span id="DDK__WMITRACE_SEARCHPATH_DBG"></span>参数


<span id="______________"></span> **+**   
将导致*TMFPath*要追加到现有的搜索路径。 如果加号 （+） 未使用令牌，则*TMFPath*替换现有的搜索路径。

<span id="_______TMFPath______"></span><span id="_______tmfpath______"></span><span id="_______TMFPATH______"></span> *TMFPath*   
调试程序应在其中查找跟踪消息格式文件的目录路径。 不支持包含空格的路径。 如果包含多个路径，它们应由分号隔开，并将整个字符串应括在引号中。 如果该路径是在引号中，必须转义字符前面的反斜杠字符 ( `"c:\\debuggers;c:\\debuggers2"` )。 当**+** 使用令牌，则*TMFPath*将以分号结束之间现有和新的路径; 自动插入追加到现有的路径，但是，如果**+** 使用令牌时，不能使用引号引起来。

<span id="_____________"></span>   

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows 2000 和更高版本的 Windows 中可用。 如果你想要 Windows 2000 中使用此扩展，您必须先将复制 Wmitrace.dll 文件的 Windows 调试工具安装目录的 winxp 子目录到 w2kfre 子目录。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。 有关跟踪消息格式化文件的信息，请参阅"跟踪消息格式化文件"主题 Windows Driver Kit (WDK) 中。

<a name="remarks"></a>备注
-------

使用不带任何参数时 **！ wmitrace.searchpath**显示当前的搜索路径。

跟踪消息格式文件 (\*.tmf) 包含用于设置跟踪提供程序生成的二进制跟踪消息的格式的说明。

*TMFPath*参数必须包含仅指向目录的路径; 它不能包含文件名称。 TMF 文件的名称是消息跟.tmf 扩展名的 GUID。 时系统设置消息的格式，它读取消息的消息的 GUID 和消息从开始到指定目录中的 GUID，其名称匹配的 TMF 文件以递归方式搜索。

Windows 需要 TMF 文件，才能在缓冲区中的二进制跟踪消息进行格式。 使用 **！ wmitrace.searchpath**或[ **！ wmitrace.tmffile** ](-wmitrace-tmffile.md)可以在使用之前指定 TMF 文件[ **！ wmitrace.dynamicprint**](-wmitrace-dynamicprint.md)或[ **！ wmitrace.logdump** ](-wmitrace-logdump.md)显示跟踪缓冲区的内容。

如果不使用 **！ wmitrace.searchpath**或[ **！ wmitrace.tmffile**](-wmitrace-tmffile.md)，则系统使用的跟踪的值\_格式\_搜索\_PATH 环境变量。 如果该变量不存在，则使用 default.tmf 文件，其中包含在 Windows 中。 如果系统找不到任何跟踪消息的格式设置信息，则它写入代替跟踪消息内容的"未找到格式信息"错误消息。

 

 





