---
title: PKEY\_FX\_Offload\_StreamEffectClsid
description: 在 Windows 10 版本 1511年及更高版本，主键\_FX\_卸载\_StreamEffectClsid 属性键标识将在卸载播放期间加载驱动程序支持的流效果 (SFX)。
ms.assetid: 2258E1F8-A96E-4991-B882-00197C2DB0B3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1e736cacd322bd8f26e0c2f81f9d3619af3093d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546267"
---
# <a name="pkeyfxoffloadstreameffectclsid"></a>PKEY\_FX\_Offload\_StreamEffectClsid


在 Windows 10 版本 1511年及更高版本，**主键\_FX\_卸载\_StreamEffectClsid**属性键标识流效果 (SFX)，将在卸载过程中加载了驱动程序支持播放。 驱动程序开发人员应指定其驱动程序支持卸载 pin 的受支持的流效果的列表。

INF 文件属性键指示音频终结点生成器 Clsid 为流效果不设置到效果属性存储以进行卸载。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件指定音频处理过程中为该设备的添加注册表部分模式效果设置。 下面的 INF 示例演示字符串并将流处理模式支持加载到注册表添加注册表部分。

```inf
[Strings]
PKEY_FX_Offload_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},11"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_STREAM_CLSID      = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.AddReg]
HKR,"FX\\0",% PKEY_FX_Offload_StreamEffectClsid %,,%FX_STREAM_CLSID%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[媒体类 INF 扩展](media-class-inf-extensions.md)










