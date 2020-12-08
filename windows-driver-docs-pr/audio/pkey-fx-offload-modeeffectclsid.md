---
title: PKEY \_ FX \_ 卸载 \_ ModeEffectClsid
description: 在 Windows 10 版本1511及更高版本中，PKEY \_ FX \_ 卸载 \_ ModeEffectClsid 键标识在卸载播放期间将加载的驱动程序支持的模式效果 (MFX) 。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95e1ef66a4dd1c237d2e40bd5fe13c9a618bc72a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800873"
---
# <a name="pkey_fx_offload_modeeffectclsid"></a>PKEY \_ FX \_ 卸载 \_ ModeEffectClsid


在 Windows 10 版本1511及更高版本中， **PKEY \_ FX \_ 卸载 \_ ModeEffectClsid** 键标识在卸载播放期间将加载的驱动程序支持的模式效果 (MFX) 。 驱动程序开发人员应指定其驱动程序支持的处理模式的列表。

INF 文件属性键指示音频终结点生成器将模式的 Clsid 设置到效果属性存储中。 此信息用于生成音频图形，该图形将用于通知高层应用程序的效果。

## <a name="span-idinf_file_samplespanspan-idinf_file_samplespanspan-idinf_file_samplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件指定该设备的 "外接程序" 部分中音频处理模式效果的设置。 以下 INF 示例显示了一些字符串和外接程序的部分，这些部分加载了 APO，用于在将卸载播放到注册表期间使用的模式效果。

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






