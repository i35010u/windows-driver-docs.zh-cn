---
title: PKEY \_ MFX \_ KeywordDetector \_ ProcessingModes \_ 支持 \_ \_ 流式处理
description: 在 Windows 10 及更高版本中 \_ ， \_ 支持流式处理属性键的 PKEY MFX KeywordDetector \_ ProcessingModes 会 \_ \_ \_ 标识驱动程序支持的流支持的关键字检测器模式效果处理模式。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1edc408ccb89aa89defcc89a1f06f20a3be424b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800863"
---
# <a name="pkey_mfx_keyworddetector_processingmodes_supported_for_streaming"></a>PKEY \_ MFX \_ KeywordDetector \_ ProcessingModes \_ 支持 \_ \_ 流式处理


在 Windows 10 及更高版本中，支持流式处理属性键的 **PKEY \_ MFX \_ KeywordDetector \_ ProcessingModes \_ \_ \_** 会标识驱动程序支持的流支持的关键字检测器模式效果处理模式。 驱动程序开发人员应列出它们的驱动程序支持的流式处理模式的关键字检测器模式效果处理模式，以便为关键字检测程序 pin 提供支持。

此列表仅包括信号处理模式，在此模式下，APO 会在流式处理期间实际处理音频信号。 此列表不得包括 APO 支持的任何信号处理模式，仅用于发现目的。

INF 文件属性键指示音频终结点生成器为中的 Clsid 设置到效果属性存储中。 此信息用于生成音频图形，该图形将用于通知高层应用程序的效果。

## <a name="span-idinf_file_samplespanspan-idinf_file_samplespanspan-idinf_file_samplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件指定该设备的 "外接程序" 部分中音频处理模式效果的设置。 以下 INF 示例显示了将关键字检测器模式效果处理模式加载到注册表中的字符串和添加注册表部分。

```inf
[Strings]
PKEY_MFX_KeywordDetector_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},9"
...
AUDIO_SIGNALPROCESSINGMODE_DEFAULT = "{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}"
AUDIO_SIGNALPROCESSINGMODE_MOVIE   = "{B26FEB0D-EC94-477C-9494-D1AB8E753F6E}"
AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS = "{98951333-B9CD-48B1-A0A3-FF40682D73F7}"
...
[SWAPAPO.I.Association0.AddReg]
;To register an APO for streaming in multiple modes, use a REG_MULTI_SZ property and include all the desired modes:
HKR,"FX\\0",%PKEY_MFX_KeywordDetector_ProcessingModes_Supported_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS%
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






