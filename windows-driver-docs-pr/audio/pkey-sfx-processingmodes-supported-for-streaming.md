---
title: '\_ \_ \_ 支持 \_ \_ 流式处理的 PKEY SFX ProcessingModes'
description: 在 Windows 8.1 及更高版本中 \_ ， \_ \_ 流属性键支持的 PKEY SFX ProcessingModes \_ \_ 标识驱动程序支持的流处理模式。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d520b5005b5c587292a1782d7f1caf7f01e7c7d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800833"
---
# <a name="pkey_sfx_processingmodes_supported_for_streaming"></a>\_ \_ \_ 支持 \_ \_ 流式处理的 PKEY SFX ProcessingModes


在 Windows 8.1 及更高版本中，流属性键 **支持的 PKEY \_ SFX \_ ProcessingModes \_ \_ \_** 标识驱动程序支持的流处理模式。 驱动程序开发人员应该列出它们的驱动程序支持的流式处理所支持的处理模式。

INF 文件属性键指示音频终结点生成器为中的 Clsid 设置到效果属性存储中。 此信息用于生成音频图形，该图形将用于通知高层应用程序的效果。

## <a name="span-idinf_file_samplespanspan-idinf_file_samplespanspan-idinf_file_samplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件指定该设备的 "外接程序" 部分中音频处理模式效果的设置。 以下 INF 示例显示了将模式效果处理模式加载到注册表中的字符串和添加注册表部分。

```inf
[Strings]
PKEY_SFX_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},5"
...
AUDIO_SIGNALPROCESSINGMODE_DEFAULT = "{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}"
AUDIO_SIGNALPROCESSINGMODE_MOVIE   = "{B26FEB0D-EC94-477C-9494-D1AB8E753F6E}"
AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS = "{98951333-B9CD-48B1-A0A3-FF40682D73F7}"
...
[SWAPAPO.I.Association0.AddReg]
;To register an APO for streaming in multiple modes, use a REG_MULTI_SZ property and include all the desired modes:
HKR,"FX\\0",%PKEY_SFX_ProcessingModes_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_COMMUNICATIONS%
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)










