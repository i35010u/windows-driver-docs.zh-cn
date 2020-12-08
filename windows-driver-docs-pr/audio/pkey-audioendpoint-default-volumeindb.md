---
title: PKEY \_ AudioEndpoint \_ 默认 \_ VolumeInDb
description: 在 Windows 10 版本1605及更高版本中，PKEY \_ AudioEndpoint \_ default \_ VolumeInDb 属性键为软件卷节点配置 dB) 中的默认卷 (。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48a10afd7dbb6fab0879838e8bc8b516993ab41d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800917"
---
# <a name="pkey_audioendpoint_default_volumeindb"></a>PKEY \_ AudioEndpoint \_ 默认 \_ VolumeInDb


在 Windows 10 版本1605及更高版本中， **PKEY \_ AudioEndpoint \_ default \_ VolumeInDb** 属性键为软件卷节点配置 dB) 中的默认卷 (。 驱动程序开发人员应提供要设置的默认 dB 值。

如果音频驱动程序未为终结点实现硬件卷节点，则 OS 将插入一个软件卷节点以控制该终结点上的卷。 有些情况下，默认的卷值太低。 此 INF 密钥向用户提供更好的体验，适用于向音频信号应用适当的增益或衰减。

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


Ihv 和 Oem 可以通过 \_ \_ \_ 使用驱动程序 INF 文件对拓扑筛选器设置 PKEY AudioEndpoint default VolumeInDb，来替代终结点的默认软件卷值。 该键指定的值以 dB 单位表示。

此密钥将用于呈现和捕获终结点。

如果终结点已实现硬件卷节点，则会忽略此项。

可以设置任何值，但 OS 将确保其值在 "最小值" 和 "最大值" 设置中。 例如，如果指定的值大于最大卷值，则 OS 会将默认值设置为 "最大容量" 值。

数据存储为16.16 固定点值。 较高的16位用于值的整数，较低的16位用于值的小数部分。

## <a name="span-idinf_file_samplespanspan-idinf_file_samplespanspan-idinf_file_samplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


```inf
; The following line overrides the default volume (in dB) for an endpoint. 
; It is only applicable when hardware volume is not implemented. 
; Decimal value expressed in fixed point 16.16 format and stored as a DWORD. 

PKEY_AudioEndpoint_Default_VolumeInDb        = "{1DA5D803-D492-4EDD-8C23-E0C0FFEE7F0E},9" 

; 10 dB 
HKR,EP\0,%PKEY_AudioEndpoint_Default_VolumeInDb%,0x00010001,0xA0000 

;-10 dB 
;HKR,EP\0,%PKEY_AudioEndpoint_Default_VolumeInDb%,0x00010001,0xFFF60000
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






