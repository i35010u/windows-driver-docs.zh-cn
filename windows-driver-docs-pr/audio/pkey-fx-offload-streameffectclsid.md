---
title: PKEY \_ FX \_ 卸载 \_ StreamEffectClsid
description: 在 Windows 10 版本1511及更高版本中，PKEY \_ FX \_ 卸载 \_ StreamEffectClsid 属性键标识在卸载播放期间将加载的驱动程序所支持的流效果 (SFX) 。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b6a8f65b99d0c22986f8027a88aab1facc68bd2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800871"
---
# <a name="pkey_fx_offload_streameffectclsid"></a>PKEY \_ FX \_ 卸载 \_ StreamEffectClsid


在 Windows 10 版本1511及更高版本中， **PKEY \_ FX \_ 卸载 \_ StreamEffectClsid** 属性键标识在卸载播放期间将加载的驱动程序所支持的流效果 (SFX) 。 驱动程序开发人员应指定其驱动程序为卸载 pin 支持的流效果的列表。

INF 文件属性键指示音频终结点生成器将流效果的 Clsid 设置为要卸载的 "效果" 属性存储。 此信息用于生成音频图形，该图形将用于通知高层应用程序的效果。

## <a name="span-idinf_file_samplespanspan-idinf_file_samplespanspan-idinf_file_samplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件指定该设备的 "外接程序" 部分中音频处理模式效果的设置。 以下 INF 示例显示了字符串和添加注册表部分，它们将支持的流处理模式加载到注册表中。

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

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)










