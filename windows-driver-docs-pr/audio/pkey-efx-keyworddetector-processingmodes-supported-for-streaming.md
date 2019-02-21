---
title: PKEY\_EFX\_KeywordDetector\_ProcessingModes\_Supported\_For\_Streaming
description: 在 Windows 10 及更高版本，主键\_EFX\_KeywordDetector\_ProcessingModes\_支持\_为\_流式处理属性键标识终结点关键字 detector 进行处理支持的流式处理驱动程序支持的模式。
ms.assetid: 517B7321-5726-4ADB-9FCD-82776B143FF9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30079680ad9364c52d3b73013262806bc1cfc532
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56548236"
---
# <a name="pkeyefxkeyworddetectorprocessingmodessupportedforstreaming"></a>PKEY\_EFX\_KeywordDetector\_ProcessingModes\_Supported\_For\_Streaming


在 Windows 10 及更高版本，**主键\_EFX\_KeywordDetector\_ProcessingModes\_支持\_有关\_流式处理**属性键标识处理模式下支持的驱动程序支持流式处理终结点关键字检测程序。 驱动程序开发人员应列出终结点处理支持的流式处理其驱动程序支持的关键字检测程序 pin 模式。

此列表仅包含其中 APO 实际处理的音频信号在流式处理过程的信号处理模式。 此列表不得包含任何信号处理仅供发现 APO 支持模式。

INF 文件属性键指示音频终结点生成器 Clsid 为未设置效果属性存储到。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

终结点影响 (EFX) 是在 tee 前面或后面之和，因为不能有多个与终结点处理关联的模式。 出于此原因，只有一个单一的模式，音频\_SIGNALPROCESSINGMODE\_默认情况下，可以指定。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件指定音频处理过程中为该设备的添加注册表部分模式效果设置。 下面的示例 INF 显示字符串和添加注册表加载流处理模式支持到注册表关键字检测程序的部分。

```inf
[Strings]
PKEY_EFX_KeywordDetector_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},10"
...
[SWAPAPO.I.Association0.AddReg]
; This line shows how to set the default processing mode for streaming.
HKR,FX\0,%PKEY_EFX_KeywordDetector_ProcessingModes_Supported_For_Streaming%,0x00010000,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






