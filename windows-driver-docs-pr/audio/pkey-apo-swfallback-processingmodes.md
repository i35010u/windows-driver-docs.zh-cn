---
title: PKEY\_APO\_SWFallback\_ProcessingModes
description: 在 Windows 10 版本 1709年及更高版本，主键\_APO\_SWFallback\_ProcessingModes 属性键标识可以回退到处理驱动程序支持的模式下的软件的 HW 模式。
ms.date: 10/22/2018
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: f1ca0b1026dba18f52644d62385fb7ac09dacf81
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567915"
---
# <a name="pkeyaposwfallbackprocessingmodes"></a>PKEY\_APO\_SWFallback\_ProcessingModes

从 Windows 10 版本 1809，开始*主键\_APO\_SWFallback\_ProcessingModes*属性键标识可以回退到软件处理的模式。 驱动程序开发人员应列出所有的处理模式下的模式影响其驱动程序支持该支持软件回退。 此列表必须包含的驱动程序支持硬件中的所有模式。

如果请求流时的以下模式之一，并且有没有足够的硬件资源可用于在该处理模式下打开 pin，pin 将在 RAW 模式中打开和使用请求的处理模式初始化 SW APO 将改为使用。 因此，想要支持软件回退的处理模式下，硬件的驱动程序必须支持 RAW 模式。 有关音频模式的详细信息，请参阅[音频信号处理模式](audio-signal-processing-modes.md)。 软件回退仅适用于主机 pin。

创建一个流，而且在硬件中没有可用资源时，会触发 SW 回退。 操作系统具备的可用资源，以确定是否需要回退的软件驱动程序的直接查询。 操作系统使用的驱动程序，如驱动程序，支持多少个 pin 实例的知识来确定如果没有足够的硬件资源。  如果硬件资源不可用软件回退用于在原始插针上创建流。 SW 回退进程由操作系统管理，并不需要输入该驱动程序软件回退发生时。 该驱动程序不需要返回任何其他特定错误代码，以使用 SWFallback。

如果已指定音频的约束，操作系统将执行对那些额外的检查。 有关详细信息，请参阅[音频硬件资源管理](audio-hardware-resource-management.md)。

该驱动程序必须在其 FxPropertyStore 有支持的回退模式。 SWFallback 任何 AUDIO_SIGNALPROCESSINGMODEs 需要添加到 PKEY_APO_SWFallback_ProcessingModes 即 {D3993A3F-99C2-4402-B5EC-A92A0367664B} 中的驱动程序 FxPropertyStore 13。 这将允许他们 SWFallback 得到认可。 



###  <a name="pkeyaposwfallbackprocessingmodes-definition"></a>PKEY\_APO\_SWFallback\_ProcessingModes Definition

*主键\_APO\_SWFallback\_ProcessingModes*定义如下所示。

```inf
PKEY_APO_SWFallback_ProcessingModes (REG_MULTI_SZ) = {D3993A3F-99C2-4402-B5EC-A92A0367664B},13 
```


### <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例

INF 文件属性键列出信号处理模式支持的主机连接器，如果有足够的硬件资源不可用，则可用于回退到 SW APO。 

INF 文件在该设备的添加注册表部分中指定的设置。 下面的示例 INF 显示字符串和将 APO 软件回退处理模式加载到注册表添加注册表部分。 在此示例中四种模式是实现，原始的默认值、 电影和通信。 

```cpp
[Strings]
PKEY_APO_SWFallback_ProcessingModes  = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},13"
...
AUDIO_SIGNALPROCESSINGMODE_DEFAULT = "{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}"
AUDIO_SIGNALPROCESSINGMODE_MOVIE   = "{B26FEB0D-EC94-477C-9494-D1AB8E753F6E}"
AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS = "{98951333-B9CD-48B1-A0A3-FF40682D73F7}"
...
[PKEY.APO.SWFallback.AddReg]
;Include all supported modes:
HKR,"FX\\0",%PKEY_APO_SWFallback_ProcessingModes%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 

[向 Microsoft 发送有关该主题的评论](mailto:wsddocfb@microsoft.com?subject=Documentation%20feedback%20[audio/audio]:%20PKEY_MFX_ProcessingModes_Supported_For_Streaming%20%20RELEASE:%20%2811/22/2017%29&body=%0A%0APRIVACY%20STATEMENT%0A%0AWe%20use%20your%20feedback%20to%20improve%20the%20documentation.%20We%20don't%20use%20your%20email%20address%20for%20any%20other%20purpose,%20and%20we'll%20remove%20your%20email%20address%20from%20our%20system%20after%20the%20issue%20that%20you're%20reporting%20is%20fixed.%20While%20we're%20working%20to%20fix%20this%20issue,%20we%20might%20send%20you%20an%20email%20message%20to%20ask%20for%20more%20info.%20Later,%20we%20might%20also%20send%20you%20an%20email%20message%20to%20let%20you%20know%20that%20we've%20addressed%20your%20feedback.%0A%0AFor%20more%20info%20about%20Microsoft's%20privacy%20policy,%20see%20 https://privacy.microsoft.com/default.aspx. "向 Microsoft 发送有关该主题的评论")





