---
title: PKEY\_SFX\_Offload\_ProcessingModes\_Supported\_For\_Streaming
description: 在 Windows 10 版本 1511年及更高版本，主键\_SFX\_卸载\_ProcessingModes\_支持\_为\_流式处理属性键标识流式处理卸载驱动程序支持的模式。
ms.assetid: 063F75D6-AA00-4096-8CFC-633A51648333
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4de8ba0947c2937b99e5212ffbdd3c9a671ad5b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328805"
---
# <a name="pkeysfxoffloadprocessingmodessupportedforstreaming"></a>PKEY\_SFX\_Offload\_ProcessingModes\_Supported\_For\_Streaming


在 Windows 10 版本 1511年及更高版本，**主键\_SFX\_卸载\_ProcessingModes\_支持\_有关\_流式处理**属性键标识流处理模式驱动程序支持卸载。 驱动程序开发人员应列出支持的卸载 pin 其驱动程序支持的卸载流处理模式。

此列表仅包含其中 APO 实际处理的音频信号期间卸载流式处理的信号处理模式。 此列表不得包含任何信号处理仅供发现 APO 支持模式。

INF 文件属性键指示设置效果属性存储到以进行卸载不 Clsid 的音频的终结点生成器。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件指定音频处理过程中为该设备的添加注册表部分模式效果设置。 下面的示例 INF 显示字符串和添加注册表加载到注册表卸载 pin 支持的流式处理模式的部分。

```inf
[Strings]
PKEY_SFX_Offload_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},11"
...
AUDIO_SIGNALPROCESSINGMODE_DEFAULT = "{C18E2F7E-933D-4965-B7D1-1EEF228D2AF3}"
AUDIO_SIGNALPROCESSINGMODE_MOVIE   = "{B26FEB0D-EC94-477C-9494-D1AB8E753F6E}"
AUDIO_SIGNALPROCESSINGMODE_MEDIA   = "{4780004E-7133-41D8-8C74-660DADD2C0EE}"
...
[SWAPAPO.I.Association0.AddReg]
;To register an APO for offload streaming in multiple modes, use a REG_MULTI_SZ property and include all the desired modes:
HKR,"FX\\0",%PKEY_SFX_Offload_ProcessingModes_Supported_For_Streaming%,%REG_MULTI_SZ%,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%,%AUDIO_SIGNALPROCESSINGMODE_MOVIE%,%AUDIO_SIGNALPROCESSINGMODE_MEDIA%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






