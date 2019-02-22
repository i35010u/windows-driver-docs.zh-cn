---
title: PKEY\_MFX\_Offload\_ProcessingModes\_Supported\_For\_Streaming
description: 在 Windows 10 版本 1511年及更高版本，主键\_MFX\_卸载\_ProcessingModes\_支持\_为\_流式处理属性键标识模式影响处理模式支持卸载流式处理驱动程序支持。
ms.assetid: 48E12E69-5159-4483-9891-2B689B7C3DCE
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7db274dbf1490b6b259a22676326bc4a6a3feda2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546287"
---
# <a name="pkeymfxoffloadprocessingmodessupportedforstreaming"></a>PKEY\_MFX\_Offload\_ProcessingModes\_Supported\_For\_Streaming


在 Windows 10 版本 1511年及更高版本，**主键\_MFX\_卸载\_ProcessingModes\_支持\_有关\_流式处理**属性键标识处理模式下支持卸载流式处理驱动程序支持的模式影响。 驱动程序开发人员应列出处理模式下支持卸载流式处理其驱动程序支持的模式影响。

INF 文件属性键指示音频终结点生成器 Clsid 为未设置效果属性存储到。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件指定音频处理过程中为该设备的添加注册表部分模式效果设置。 下面的示例 INF 显示字符串和加载流处理模式支持到注册表卸载添加注册表部分。

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






