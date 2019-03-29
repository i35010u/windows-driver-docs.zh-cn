---
title: PKEY\_FX\_KeywordDetector\_StreamEffectClsid
description: 在 Windows 10 及更高版本，主键\_FX\_KeywordDetector\_StreamEffectClsid 属性键标识流效果 (SFX) 支持关键字检测程序的驱动程序。
ms.assetid: C4ED26A0-FDFB-499B-8A61-429E53CCAE6A
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fee9f8ab71264773be7b1a970878db19afdd0d71
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563016"
---
# <a name="pkeyfxkeyworddetectorstreameffectclsid"></a>PKEY\_FX\_KeywordDetector\_StreamEffectClsid


在 Windows 10 及更高版本，**主键\_FX\_KeywordDetector\_StreamEffectClsid**属性键标识流效果 (SFX) 支持关键字检测程序的驱动程序。 驱动程序开发人员应指定其驱动程序支持的关键字检测器 pin 的单个流效果。

INF 文件属性键指示设置效果属性存储到的终结点不 Clsid 的音频的终结点生成器。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件在该设备的添加注册表部分中指定音频端点设备的设置。 下面的示例 INF 显示字符串和将关键字检测程序流效果 APO 加载到注册表添加注册表部分。

```inf
[Strings]
PKEY_FX_KeywordDetector_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},8"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_KEYWORD_STREAM_CLSID      = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.AddReg]
HKR,"FX\\0",%PKEY_FX_KeywordDetector_StreamEffectClsid%,,%FX_KEYWORD_STREAM_CLSID%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






