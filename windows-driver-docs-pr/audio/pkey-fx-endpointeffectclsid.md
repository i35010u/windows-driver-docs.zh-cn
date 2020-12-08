---
title: PKEY \_ FX \_ EndpointEffectClsid
description: 在 Windows 8.1 和更高版本中，PKEY \_ FX \_ EndpointEffectClsid 属性键用于标识 (EFX) 位置的终结点效果。 驱动程序开发人员应指定其驱动程序支持的处理模式的列表。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b909332a05ff11920a8683dc741b71155f35f149
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800889"
---
# <a name="pkey_fx_endpointeffectclsid"></a>PKEY \_ FX \_ EndpointEffectClsid


在 Windows 8.1 和更高版本中， **PKEY \_ FX \_ EndpointEffectClsid** 属性键用于标识 (EFX) 位置的终结点效果。 驱动程序开发人员应指定其驱动程序支持的处理模式的列表。

INF 文件属性键指示音频终结点生成器将终结点的 Clsid 设置为影响属性存储区。 此信息用于生成音频图形，该图形将用于通知高层应用程序的效果。

## <a name="span-idinf_file_samplespanspan-idinf_file_samplespanspan-idinf_file_samplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件在该设备的 "外接程序" 部分中指定音频终结点设备的默认格式。 以下 INF 示例显示了用于将终结点效果的 APO 加载到注册表中的字符串和添加注册表部分。

```inf
[Strings]
PKEY_FX_EndpointEffectClsid = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},7"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_ENDPOINT_CLSID               = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.I.Association0.AddReg]
HKR,"FX\\0",%PKEY_FX_EndpointEffectClsid%,,%FX_ENDPOINT_CLSID%
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






