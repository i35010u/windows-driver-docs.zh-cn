---
title: PKEY\_CompositeFX\_StreamEffectClsid
description: 在 Windows 10 版本 1803年和更高版本，主键\_FX\_StreamEffectClsid 属性键标识流效果 (SCompositeFX) 驱动程序支持。 驱动程序开发人员应指定其驱动程序支持的受支持的流效果的列表。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: c9c37a48e93ed438705e240bfb29869d17329b84
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525277"
---
# <a name="pkeycompositefxstreameffectclsid"></a>PKEY\_CompositeFX\_StreamEffectClsid


在 Windows 10 版本 1803年和更高版本，**主键\_CompositeFX\_StreamEffectClsid**属性键标识流效果 (SCompositeFX) 驱动程序支持。 驱动程序开发人员应指定其驱动程序支持的受支持的流效果的列表。

此属性键等同于[主键\_FX\_StreamEffectClsid](pkey-fx-streameffectclsid.md)属性键，但它是在注册表中以允许在单个位置中的多个效果表示为 reg 多字符串复合。

INF 文件属性键指示设置效果属性存储到的终结点不 Clsid 的音频的终结点生成器。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件在该设备的添加注册表部分中指定音频端点设备的设置。 下面的 INF 示例演示字符串并将流效果 APO 加载到注册表添加注册表部分。

```inf
[Strings]
PKEY_CompositeFX_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},13"
...
; Driver developers should replace this CLSIDs with that of their own APO
SWAP_FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
DELAY_FX_STREAM_CLSID   = "{00000000-0000-0000-0000-000000000000}"
...
 
[SWAPAPO.I.Association0.AddReg]
HKR,FX\0,%PKEY_CompositeFX_StreamEffectClsid%,0x00010000,%SWAP_FX_MODE_CLSID%,%DELAY_FX_MODE_CLSID%

```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






