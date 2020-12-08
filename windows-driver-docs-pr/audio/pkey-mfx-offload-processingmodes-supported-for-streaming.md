---
title: PKEY \_ MFX \_ 卸载 \_ ProcessingModes \_ 支持 \_ \_ 流式处理
description: 在 Windows 10 版本1511及更高版本中， \_ \_ 支持流式处理属性键的 PKEY MFX 卸载 \_ ProcessingModes \_ \_ \_ 标识驱动程序支持的卸载流式处理模式的处理模式。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1eff381ca7620ada79c600f365fea57865106a3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800857"
---
# <a name="pkey_mfx_offload_processingmodes_supported_for_streaming"></a>PKEY \_ MFX \_ 卸载 \_ ProcessingModes \_ 支持 \_ \_ 流式处理


在 Windows 10 版本1511及更高版本中，支持流式处理属性键的 **PKEY \_ MFX \_ 卸载 \_ ProcessingModes \_ \_ \_** 标识驱动程序支持的卸载流式处理模式的处理模式。 驱动程序开发人员应列出其驱动程序支持的卸载流式处理所支持的模式效果处理模式。

INF 文件属性键指示音频终结点生成器为中的 Clsid 设置到效果属性存储中。 此信息用于生成音频图形，该图形将用于通知高层应用程序的效果。

## <a name="span-idinf_file_samplespanspan-idinf_file_samplespanspan-idinf_file_samplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件指定该设备的 "外接程序" 部分中音频处理模式效果的设置。 以下 INF 示例显示了字符串和添加注册表部分，这些部分将支持的卸载流处理模式加载到注册表中。

```inf
[Strings]
PKEY_MFX_Offload_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},12"
...
AUDIO_SIGNALPROCESSINGMODE_DEFAULT = "{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}"
AUDIO_SIGNALPROCESSINGMODE_MOVIE   = "{B26FEB0D-EC94-477C-9494-D1AB8E753F6E}"
AUDIO_SIGNALPROCESSINGMODE_MEDIA   = "{4780004E-7133-41D8-8C74-660DADD2C0EE}"

...
[SWAPAPO.I.Association0.AddReg]
;To register an APO for streaming in multiple modes, use a REG_MULTI_SZ property and include all the desired modes:
HKR,"FX\\0",%PKEY_MFX_Offload_ProcessingModes_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_MEDIA%
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






