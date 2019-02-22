---
title: PKEY\_CompositeFX\_EndpointEffectClsid
description: 在 Windows 10 版本 1803年和更高版本，主键\_CompositeFX\_EndpointEffectClsid 属性键就地标识终结点生效 (EFX)。
ms.date: 11/15/2018
ms.localizationpriority: medium
ms.openlocfilehash: b168588541d252701e64b6aae6bbb793df15a0fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546366"
---
# <a name="pkeycompositefxendpointeffectclsid"></a>PKEY\_CompositeFX\_EndpointEffectClsid

在 Windows 版本 1803年和更高版本，**主键\_CompositeFX\_EndpointEffectClsid**属性键就地标识终结点效果 (EFX)。 驱动程序开发人员应指定其驱动程序支持的受支持的处理模式的列表。

此属性键等同于[主键\_FX\_EndpointEffectClsid](pkey-fx-endpointeffectclsid.md)属性键，但它是在注册表中以允许在单个位置中的多个效果表示为 reg 多字符串复合.

INF 文件属性键指示音频终结点生成器 Clsid 为终结点未设置效果属性存储到。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例

INF 文件在该设备，添加注册表部分中指定音频端点设备的默认格式。 下面的 INF 示例演示字符串并将终结点效果 APO 加载到注册表添加注册表部分。

```inf
[Strings]
PKEY_CompositeFX_EndpointEffectClsid = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},15"
...

SWAP_FX_MODE_CLSID      = "{00000000-0000-0000-0000-000000000000}"
DELAY_FX_STREAM_CLSID   = "{00000000-0000-0000-0000-000000000000}"
...
 
[SWAPAPO.I.Association0.AddReg]
HKR,FX\0,%PKEY_CompositeFX_EndpointEffectClsid%,0x00010000,%SWAP_FX_MODE_CLSID%,%DELAY_FX_MODE_CLSID%

```


## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题

[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






