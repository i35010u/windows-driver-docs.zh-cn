---
title: PKEY\_AudioEndpoint\_Default\_VolumeInDb
description: 在 Windows 10 版本 1605年及更高版本，主键\_AudioEndpoint\_默认\_VolumeInDb 属性注册表项配置软件卷节点的默认卷 （dB) 中。
ms.assetid: 9BC8E0D1-F4F3-4FB4-A50F-E4C79317EC30
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ca015eef0f924bb780b7f8f2dfac97429384a688
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576682"
---
# <a name="pkeyaudioendpointdefaultvolumeindb"></a>PKEY\_AudioEndpoint\_Default\_VolumeInDb


Windows 10 版本 1605年中及更高版本，**主键\_AudioEndpoint\_默认\_VolumeInDb**属性注册表项配置软件卷节点的默认卷 （dB) 中。 驱动程序开发人员应提供他们想要设置的默认 dB 值。

如果音频驱动程序未实现的终结点的硬件卷节点，操作系统将插入软件卷节点来控制该终结点上的卷。 有些情况下，默认音量值是过低。 相应的收益或衰减应用到音频信号时，此 INF 密钥提供用户更好的体验。

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


Ihv 和 Oem 可以通过设置主键替代终结点的默认软件卷值\_AudioEndpoint\_默认\_VolumeInDb 使用驱动程序 INF 文件对拓扑筛选器。 由参数指定的值是以数据库单位。

此密钥将用于这两个呈现器，并捕获终结点。

如果终结点已实现硬件卷节点，则忽略此密钥。

可以设置任何值，但操作系统将确保值中的最小值和最大值设置。 例如，如果指定的值大于最大音量值，OS 将将默认值设置为最大音量值。

数据存储为 16.16 固定的点值。 较高的 16 位用于值的整数，低 16 位适用值的小数部分。

## <a name="span-idinffilesamplespanspan-idinffilesamplespanspan-idinffilesamplespaninf-file-sample"></a><span id="INF_File_Sample"></span><span id="inf_file_sample"></span><span id="INF_FILE_SAMPLE"></span>INF 文件示例


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

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[媒体类 INF 扩展](media-class-inf-extensions.md)

 

 






