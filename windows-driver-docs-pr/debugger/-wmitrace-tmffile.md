---
title: wmitrace.tmffile
description: Tmffile 扩展 (TMF) 文件指定跟踪消息格式。 此扩展指定的文件用于格式化由其他 WMI 跟踪扩展显示或写入的跟踪消息。
keywords:
- wmitrace tmffile Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wmitrace.tmffile
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 13b4c962d541948c92d922d085f6c6105671ac5a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819357"
---
# <a name="wmitracetmffile"></a>!wmitrace.tmffile


**！ Wmitrace tmffile** (TMF) 文件中指定跟踪消息格式。 此扩展指定的文件用于格式化由其他 WMI 跟踪扩展显示或写入的跟踪消息。

```dbgcmd
!wmitrace.tmffile TMFFile 
```

## <a name="span-idddk__wmitrace_tmffile_dbgspanspan-idddk__wmitrace_tmffile_dbgspanparameters"></a><span id="ddk__wmitrace_tmffile_dbg"></span><span id="DDK__WMITRACE_TMFFILE_DBG"></span>参数


<span id="_______TMFFile______"></span><span id="_______tmffile______"></span><span id="_______TMFFILE______"></span>*TMFFile*   
指定跟踪消息格式的文件。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

此扩展由 Wmitrace.dll 导出。

此扩展在 windows 2000 和更高版本的 Windows 中可用。 如果要将此扩展与 Windows 2000 一起使用，必须先将 Wmitrace.dll 文件从 Windows 的调试工具安装目录的 winxp 子目录复制到 w2kfre 子目录。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关事件跟踪的概念性概述，请参阅 Microsoft Windows SDK。 有关跟踪消息格式文件的信息，请参阅 Windows 驱动程序工具包 (WDK) 中的 "跟踪消息格式文件" 主题。

<a name="remarks"></a>备注
-------

*跟踪消息格式文件* () 是在 Windows 软件跟踪预处理器 (WPP) 软件跟踪过程中创建的结构化文本文件。 这些文件包含有关设置跟踪二进制跟踪消息格式的说明，以便可以在用户可读的窗体中显示这些消息。

若要在跟踪缓冲区 ([**！ logdump**](-wmitrace-logdump.md)) 中显示跟踪消息，或将跟踪消息写入 [**(！ wmitrace logsave**](-wmitrace-logsave.md)) ，必须首先为跟踪消息标识 TMF 文件。

可以使用 [**！ wmitrace**](-wmitrace-searchpath.md) 指定存储 TMF 文件的目录。 然后，系统会在目录中搜索 TMF 文件，其中包含有关要设置格式的消息的说明。  (它使用消息 GUID 将消息与正确的 TMF 文件相关联。 ) 

不过，你可以使用 **！ wmitrace** 来指定特定的 TMF 文件。 如果 TMF 文件名不是消息 GUID 后跟 TMF 扩展名，则必须使用 **！ wmitrace. tmffile** 。 否则，系统将找不到该文件。

如果不使用任何一个 [**！ wmitrace**](-wmitrace-searchpath.md) 或 **tmffile**，系统将使用跟踪 \_ 格式 \_ 搜索 \_ 路径环境变量的值。 如果该变量不存在，则使用 tmf 文件。 如果系统无法找到跟踪消息的格式设置信息，则它将写入 "未找到格式信息" 错误消息，而不是跟踪消息内容。

**注意**  如果驱动程序使用的是 UMDF 1.11 版或更高版本，则不需要使用 [**！ wmitrace**](-wmitrace-searchpath.md) 或 **tmffile**。

 

此扩展仅在 WPP 软件跟踪过程中有用，更早 (适用于 Windows 的事件跟踪的旧) 方法。 其他类提供程序生成的跟踪事件不会使用跟踪消息格式 (TMF) 文件，因此不能对其使用此扩展。

 

 





