---
title: PKEY\_FX\_ModeEffectClsid
description: 在 Windows 8.1 及更高版本，主键\_FX\_ModeEffectClsid 属性键标识模式效果 (MFX) 驱动程序支持。 驱动程序开发人员应指定其驱动程序支持的受支持的处理模式的列表。
ms.assetid: 0B15A817-5F49-45B6-AD82-95738C4FF59C
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9639b437aba328403602ee97f5d8db5fc334296
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332097"
---
# <a name="pkeyfxmodeeffectclsid"></a>PKEY\_FX\_ModeEffectClsid


Windows 8.1 及更高版本，**主键\_FX\_ModeEffectClsid**属性键标识模式效果 (MFX) 驱动程序支持。 驱动程序开发人员应指定其驱动程序支持的受支持的处理模式的列表。

INF 文件属性键指示设置效果属性存储到的终结点不 Clsid 的音频的终结点生成器。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件在该设备的添加注册表部分中指定的音频模式效果的设置。 下面的示例 INF 显示字符串和将模式效果 APO 加载到注册表添加注册表部分。

```inf
[Strings]
PKEY_FX_ModeEffectClsid     = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},6"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.I.Association0.AddReg]
HKR,"FX\\0",%PKEY_FX_ModeEffectClsid%,,%FX_MODE_CLSID%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






