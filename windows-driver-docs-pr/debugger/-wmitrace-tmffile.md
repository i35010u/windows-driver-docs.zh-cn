---
title: wmitrace.tmffile
description: Wmitrace.tmffile 扩展指定的跟踪消息格式 (TMF) 文件。 此扩展插件指定的文件用于设置格式显示或写入的其他 WMI 跟踪扩展的跟踪消息。
ms.assetid: 37ad335b-7604-466b-b328-7aebbc2fb5c1
keywords:
- wmitrace.tmffile Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.tmffile
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e59697564d43fb52c23aa1dabd3a5e99bb39a684
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525041"
---
# <a name="wmitracetmffile"></a>!wmitrace.tmffile


**！ Wmitrace.tmffile**扩展指定可在跟踪消息格式 (TMF) 文件。 此扩展插件指定的文件用于设置格式显示或写入的其他 WMI 跟踪扩展的跟踪消息。

```dbgcmd
!wmitrace.tmffile TMFFile 
```

## <a name="span-idddkwmitracetmffiledbgspanspan-idddkwmitracetmffiledbgspanparameters"></a><span id="ddk__wmitrace_tmffile_dbg"></span><span id="DDK__WMITRACE_TMFFILE_DBG"></span>参数


<span id="_______TMFFile______"></span><span id="_______tmffile______"></span><span id="_______TMFFILE______"></span> *TMFFile*   
指定跟踪消息格式化文件。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展插件导出的 Wmitrace.dll。

此扩展是在 Windows 2000 和更高版本的 Windows 中可用。 如果你想要 Windows 2000 中使用此扩展，您必须先将复制 Wmitrace.dll 文件的 Windows 调试工具安装目录的 winxp 子目录到 w2kfre 子目录。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

事件跟踪的概念概述，请参阅 Microsoft Windows SDK。 有关跟踪消息格式化文件的信息，请参阅"跟踪消息格式化文件"主题 Windows Driver Kit (WDK) 中。

<a name="remarks"></a>备注
-------

*跟踪消息格式文件*(.tmf) 是在 Windows 软件跟踪预处理器 (WPP) 软件跟踪过程中创建的结构化的文本文件。 这些文件包含有关格式设置跟踪二进制跟踪消息的说明，以便它们可以人工可读的窗体中显示。

为了在跟踪缓冲区中显示跟踪消息 ([**！ wmitrace.logdump**](-wmitrace-logdump.md)) 或将其写入到文件[ **(！ wmitrace.logsave**](-wmitrace-logsave.md))，您必须首先确定跟踪消息的 TMF 文件。

可以使用[ **！ wmitrace.searchpath** ](-wmitrace-searchpath.md)用于指定在哪个 TMF 文件存储的目录。 系统然后搜索包含正在设置格式的消息说明的 TMF 文件的目录。 （它使用消息 GUID 来将消息与正确的 TMF 文件相关联。）

但是，可以使用 **！ wmitrace.tmffile**来指定特定的 TMF 文件。 必须使用 **！ wmitrace.tmffile**如果 TMF 文件名称不是一条消息后加.tmf 扩展名的 GUID。 否则，系统将不到它。

如果不使用[ **！ wmitrace.searchpath** ](-wmitrace-searchpath.md)或 **！ wmitrace.tmffile**，则系统使用的跟踪的值\_格式\_搜索\_PATH 环境变量。 如果该变量不存在，则使用 default.tmf 文件。 如果系统找不到跟踪消息的格式设置信息，则它写入"未找到格式信息"错误消息，而不是跟踪消息内容。

**请注意**  如果您的驱动程序使用 UMDF 版本 1.11 或更高版本，不需要使用[ **！ wmitrace.searchpath** ](-wmitrace-searchpath.md)或者 **！ wmitrace.tmffile**。

 

此扩展在 WPP 软件跟踪和早期的 Windows 事件跟踪 （旧版） 方法期间才有用。 其他清单表示提供程序生成的跟踪事件不使用跟踪消息格式 (TMF) 文件，并因此不能与它们使用此扩展。

 

 





