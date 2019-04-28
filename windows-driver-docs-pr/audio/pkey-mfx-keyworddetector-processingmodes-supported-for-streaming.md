---
title: PKEY\_MFX\_KeywordDetector\_ProcessingModes\_Supported\_For\_Streaming
description: 在 Windows 10 及更高版本，主键\_MFX\_KeywordDetector\_ProcessingModes\_支持\_为\_流式处理属性键标识关键字检测器模式效果支持的流式处理驱动程序支持的处理模式。
ms.assetid: 17DEDF05-482C-44A8-91E8-50AF252F540D
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 16cffac2f95c2c64260e62be11e55c972d13fcae
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332181"
---
# <a name="pkeymfxkeyworddetectorprocessingmodessupportedforstreaming"></a>PKEY\_MFX\_KeywordDetector\_ProcessingModes\_Supported\_For\_Streaming


在 Windows 10 及更高版本，**主键\_MFX\_KeywordDetector\_ProcessingModes\_支持\_有关\_流式处理**属性键标识关键字检测器模式效果处理支持流式处理驱动程序支持的模式。 驱动程序开发人员应列出关键字检测器模式影响处理支持的流式处理其驱动程序支持的关键字检测程序 pin 模式。

此列表仅包含其中 APO 实际处理的音频信号在流式处理过程的信号处理模式。 此列表不得包含任何信号处理仅供发现 APO 支持模式。

INF 文件属性键指示音频终结点生成器 Clsid 为未设置效果属性存储到。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件指定音频处理过程中为该设备的添加注册表部分模式效果设置。 下面的示例 INF 显示字符串和添加注册表加载到注册表处理模式下的关键字检测器模式影响的部分。

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






