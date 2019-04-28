---
title: PKEY\_FX\_StreamEffectClsid
description: 在 Windows 8.1 及更高版本，主键\_FX\_StreamEffectClsid 属性键标识流效果 (SFX) 驱动程序支持。 驱动程序开发人员应指定其驱动程序支持的受支持的流效果的列表。
ms.assetid: 8557AE39-56DF-4184-A74A-186AF30F2A63
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 407b86451b547a28cab88bd7ca4db9e9f5a3d182
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332139"
---
# <a name="pkeyfxstreameffectclsid"></a>PKEY\_FX\_StreamEffectClsid


Windows 8.1 及更高版本，**主键\_FX\_StreamEffectClsid**属性键标识流效果 (SFX) 驱动程序支持。 驱动程序开发人员应指定其驱动程序支持的受支持的流效果的列表。

INF 文件属性键指示设置效果属性存储到的终结点不 Clsid 的音频的终结点生成器。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件在该设备的添加注册表部分中指定音频端点设备的设置。 下面的 INF 示例演示字符串并将流效果 APO 加载到注册表添加注册表部分。

```inf
[Strings]
PKEY_FX_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},5"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_STREAM_CLSID      = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.AddReg]
HKR,"FX\\0",%PKEY_FX_StreamEffectClsid%,,%FX_STREAM_CLSID%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






