---
title: PKEY\_EFX\_ProcessingModes\_Supported\_For\_Streaming
description: 在 Windows 8.1 及更高版本，主键\_EFX\_ProcessingModes\_支持\_为\_流式处理属性键标识处理模式下支持的驱动程序支持流式处理终结点.
ms.assetid: AE905F16-3065-4D7C-A535-143EB77812C9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a2520efb1a0fd2a62223c29843f364af987f35d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520112"
---
# <a name="pkeyefxprocessingmodessupportedforstreaming"></a>PKEY\_EFX\_ProcessingModes\_Supported\_For\_Streaming


Windows 8.1 及更高版本，**主键\_EFX\_ProcessingModes\_支持\_有关\_流式处理**属性键标识终结点处理模式支持流式处理驱动程序支持。 驱动程序开发人员应列出处理模式下支持流式处理终结点，其驱动程序支持。

INF 文件属性键指示音频终结点生成器 Clsid 为未设置效果属性存储到。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

终结点影响 (EFX) 是在 tee 前面或后面之和，因为不能有多个与终结点处理关联的模式。 出于此原因，只有一个单一的模式，音频\_SIGNALPROCESSINGMODE\_默认情况下，可以指定。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件指定音频处理过程中为该设备的添加注册表部分模式效果设置。 下面的 INF 示例演示字符串并将流处理模式支持加载到注册表添加注册表部分。

```inf
[Strings]
PKEY_EFX_ProcessingModes_Supported_For_Streaming = "{D3993A3F-99C2-4402-B5EC-A92A0367664B},7"
...
[SWAPAPO.I.Association0.AddReg]
; This line shows how to set the default processing mode for streaming.
HKR,FX\0,%PKEY_EFX_ProcessingModes_Supported_For_Streaming%,0x00010000,%AUDIO_SIGNALPROCESSINGMODE_DEFAULT%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






