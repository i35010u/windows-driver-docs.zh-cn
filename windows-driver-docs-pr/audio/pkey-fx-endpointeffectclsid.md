---
title: PKEY\_FX\_EndpointEffectClsid
description: 在 Windows 8.1 及更高版本，主键\_FX\_EndpointEffectClsid 属性键就地标识终结点生效 (EFX)。 驱动程序开发人员应指定其驱动程序支持的受支持的处理模式的列表。
ms.assetid: 19E92978-12DE-4B0E-A386-024B88A64B39
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22811ba13a6b449e237f939e087280b01887e20c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523564"
---
# <a name="pkeyfxendpointeffectclsid"></a>PKEY\_FX\_EndpointEffectClsid


Windows 8.1 及更高版本，**主键\_FX\_EndpointEffectClsid**属性键就地标识终结点生效 (EFX)。 驱动程序开发人员应指定其驱动程序支持的受支持的处理模式的列表。

INF 文件属性键指示音频终结点生成器 Clsid 为终结点未设置效果属性存储到。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件在该设备，添加注册表部分中指定音频端点设备的默认格式。 下面的 INF 示例演示字符串并将终结点有效 APO 加载到注册表添加注册表部分。

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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






