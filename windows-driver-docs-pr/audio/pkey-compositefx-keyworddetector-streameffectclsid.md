---
title: PKEY\_CompositeFX\_KeywordDetector\_StreamEffectClsid
description: 在 Windows 10 版本 1803年和更高版本，主键\_CompositeFX\_KeywordDetector\_StreamEffectClsid 属性键标识流效果 (SFX) 支持关键字检测程序的驱动程序。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6dfe603ebfdf3091080bc5b4c2eaff388128cdc6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567854"
---
# <a name="pkeycompositefxkeyworddetectorstreameffectclsid"></a>PKEY\_CompositeFX\_KeywordDetector\_StreamEffectClsid

在 Windows 10 版本 1803年和更高版本，**主键\_CompositeFX\_KeywordDetector\_StreamEffectClsid**属性键标识支持的关键字检测器流效果 (SFX)驱动程序。 驱动程序开发人员应指定其驱动程序支持的关键字检测器 pin 的单个流效果。

此属性键等同于[主键\_FX\_KeywordDetector\_StreamEffectClsid](pkey-fx-keyworddetector-streameffectclsid.md)属性键，但它是以允许在注册表中表示为 reg 多字符串复合在单个位置中的多个效果。 

INF 文件属性键指示设置效果属性存储到的终结点不 Clsid 的音频的终结点生成器。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。


## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例

INF 文件在该设备的添加注册表部分中指定音频端点设备的设置。 下面的示例 INF 显示字符串和将关键字检测程序流效果 APO 加载到注册表添加注册表部分。

```inf
[Strings]
PKEY_CompositeFX_KeywordDetector_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},16"
...
; Driver developers should replace this CLSIDs with that of their own APO
SWAP_FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
DELAY_FX_STREAM_CLSID   = "{00000000-0000-0000-0000-000000000000}"
...
 
[SWAPAPO.I.Association0.AddReg]
HKR,FX\0,%PKEY_CompositeFX_KeywordDetector_StreamEffectClsid%,0x00010000,%SWAP_FX_MODE_CLSID%,%DELAY_FX_MODE_CLSID%

```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






