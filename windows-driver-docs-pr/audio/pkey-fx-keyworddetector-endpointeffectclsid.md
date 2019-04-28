---
title: PKEY\_FX\_KeywordDetector\_EndpointEffectClsid
description: 在 Windows 10 及更高版本，主键\_FX\_KeywordDetector\_EndpointEffectClsid 属性键就地标识关键字检测程序终结点效果 (EFX)。
ms.assetid: 2D776DB4-A317-4097-B188-65CA495D0F89
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb0ed082502892fde4d872e146c01e613359a8d5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332126"
---
# <a name="pkeyfxkeyworddetectorendpointeffectclsid"></a>PKEY\_FX\_KeywordDetector\_EndpointEffectClsid


在 Windows 10 及更高版本，**主键\_FX\_KeywordDetector\_EndpointEffectClsid**属性键就地标识关键字检测程序终结点效果 (EFX)。 驱动程序开发人员应指定其驱动程序支持的关键字检测器 pin 的单一支持的处理模式。

INF 文件属性键指示音频终结点生成器 Clsid 为终结点未设置效果属性存储到。 此信息用于生成在音频图形的将用来通知哪些因素影响均已到位的上部级别应用。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


INF 文件在该设备，添加注册表部分中指定音频端点设备的默认格式。 下面的 INF 示例演示字符串并将终结点关键字检测器效果 APO 加载到注册表添加注册表部分。

```inf
[Strings]
PKEY_FX_KeywordDetector_EndpointEffectClsid = "{D04E05A6-594B-4fb6-A80D-01AF5EED7D1D},10"
...
; Driver developers should replace this CLSIDs with that of their own APO
FX_KEYWORD_ENDPOINT_CLSID               = "{00000000-0000-0000-0000-000000000000}"
...
[SWAPAPO.I.Association0.AddReg]
HKR,"FX\\0",%PKEY_FX_KeywordDetector_EndpointEffectClsid%,,%FX_KEYWORD_ENDPOINT_CLSID%
```

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






