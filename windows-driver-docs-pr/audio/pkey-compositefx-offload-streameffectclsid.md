---
title: PKEY\_CompositeFX\_Offload\_StreamEffectClsid
description: 在 Windows 10，版本 1803年和更高版本，主键\_CompositeFX\_卸载\_StreamEffectClsid 属性键标识流效果 (SFX) 驱动程序支持。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: ed2efb03b558eba084cda7aee5dbd7007cd6f05d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564665"
---
# <a name="pkeycompositefxoffloadstreameffectclsid"></a>PKEY\_CompositeFX\_Offload\_StreamEffectClsid


在 Windows 10，版本 1803年和更高版本，**主键\_CompositeFX\_卸载\_StreamEffectClsid**属性键标识流效果 (SFX) 将加载驱动程序支持在卸载播放。 驱动程序开发人员应指定其驱动程序支持卸载 pin 的受支持的流效果的列表。

此属性键等同于[主键\_FX\_卸载\_StreamEffectClsid](pkey-fx-offload-streameffectclsid.md)属性键，但它是在注册表中以允许多个表示为 reg 多字符串复合在单个位置中的效果。

INF 文件属性键指示音频终结点生成器 Clsid 为流效果不设置到效果属性存储以进行卸载。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例

INF 文件指定音频处理过程中为该设备的添加注册表部分模式效果设置。 下面的 INF 示例演示字符串并将流处理模式支持加载到注册表添加注册表部分。

```inf
[Strings]
PKEY_CompositeFX_Offload_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},11"
...
; Driver developers should replace this CLSIDs with that of their own APO
SWAP_FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
DELAY_FX_STREAM_CLSID   = "{00000000-0000-0000-0000-000000000000}"
...
 
[SWAPAPO.I.Association0.AddReg]
HKR,FX\0,%PKEY_CompositeFX_Offload_StreamEffectClsid%,0x00010000,%SWAP_FX_MODE_CLSID%,%DELAY_FX_MODE_CLSID%


```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






