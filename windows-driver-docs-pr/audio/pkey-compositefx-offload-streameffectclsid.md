---
title: PKEY\_CompositeFX\_卸载\_StreamEffectClsid
description: 在 Windows 10 版本1803及更高版本中，PKEY\_CompositeFX\_卸载\_StreamEffectClsid 属性键标识驱动程序所支持的流效果（SFX）。
ms.date: 01/07/2020
ms.localizationpriority: medium
ms.openlocfilehash: 97c5a1f9bee50d903f73e3b424791665ddc72864
ms.sourcegitcommit: 09a1ef35029216ce98510ae8794c957157d9688e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2020
ms.locfileid: "75727776"
---
# <a name="pkey_compositefx_offload_streameffectclsid"></a>PKEY\_CompositeFX\_卸载\_StreamEffectClsid

在 Windows 10 版本1803及更高版本中， **PKEY\_CompositeFX\_卸载\_StreamEffectClsid**属性键标识在卸载播放过程中将加载的驱动程序所支持的流效果（SFX）。 驱动程序开发人员应指定其驱动程序为卸载 pin 支持的流效果的列表。

此属性键与[PKEY\_FX\_卸载\_StreamEffectClsid](pkey-fx-offload-streameffectclsid.md)属性键相同，但它是一个复合，表示为注册表中的 reg 多字符串，以允许在一个位置中使用多个效果。

INF 文件属性键指示音频终结点生成器将流效果的 Clsid 设置为要卸载的 "效果" 属性存储。 此信息用于生成音频图形，该图形将用于通知高层应用程序的效果。

## <a name="span-idinf_file_samplespanspan-idinf_file_samplespanspan-idinf_file_samplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例

INF 文件指定该设备的 "外接程序" 部分中音频处理模式效果的设置。 以下 INF 示例显示了字符串和添加注册表部分，它们将支持的流处理模式加载到注册表中。

```inf
[Strings]
PKEY_CompositeFX_Offload_StreamEffectClsid   = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},19"
...
; Driver developers should replace this CLSIDs with that of their own APO
SWAP_FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
DELAY_FX_STREAM_CLSID   = "{00000000-0000-0000-0000-000000000000}"
...

[SWAPAPO.I.Association0.AddReg]
HKR,FX\0,%PKEY_CompositeFX_Offload_StreamEffectClsid%,0x00010000,%SWAP_FX_MODE_CLSID%,%DELAY_FX_MODE_CLSID%


```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题

[媒体类 INF 扩展](media-class-inf-extensions.md)
