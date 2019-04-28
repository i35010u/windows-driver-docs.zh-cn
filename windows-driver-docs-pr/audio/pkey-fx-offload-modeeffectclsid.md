---
title: PKEY\_FX\_Offload\_ModeEffectClsid
description: 在 Windows 10 版本 1511年及更高版本，主键\_FX\_卸载\_ModeEffectClsid 键标识将在卸载播放期间加载驱动程序支持的模式效果 (MFX)。
ms.assetid: DAA40089-4762-4D26-BEE1-99C1D19783C3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8bf468eaff400bfa3657b182ca86a8b14aa7fc36
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332163"
---
# <a name="pkeyfxoffloadmodeeffectclsid"></a>PKEY\_FX\_Offload\_ModeEffectClsid


在 Windows 10 版本 1511年及更高版本，**主键\_FX\_卸载\_ModeEffectClsid**键标识将在卸载播放期间加载驱动程序支持的模式效果 (MFX)。 驱动程序开发人员应指定其驱动程序支持的受支持的处理模式的列表。

INF 文件属性键指示音频终结点生成器 Clsid 为模式未设置效果属性存储到。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件指定音频处理过程中为该设备的添加注册表部分模式效果设置。 下面的示例 INF 显示字符串和添加注册表部分加载模式效果 APO 期间要使用的负载卸载到注册表的播放。

```inf
[Strings]
PKEY_FX_Offload_ModeEffectClsid     = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},12"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.I.Association0.AddReg]
HKR,"FX\\0",%PKEY_FX_Offload_ModeEffectClsid%,,%FX_MODE_CLSID%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






