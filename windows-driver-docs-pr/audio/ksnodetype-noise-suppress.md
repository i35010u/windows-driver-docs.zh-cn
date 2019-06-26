---
title: KSNODETYPE\_干扰\_禁止
description: KSNODETYPE\_干扰\_禁止
ms.assetid: 416504e2-38eb-4cfd-ae20-6f1f44a82abd
keywords:
- KSNODETYPE_NOISE_SUPPRESS 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_NOISE_SUPPRESS
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e8ab8c7a3ab1eb4358c9f70d5d53fef6bef4e75
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359020"
---
# <a name="ksnodetypenoisesuppress"></a>KSNODETYPE\_干扰\_禁止


## <span id="ddk_ksnodetype_noise_suppress_ks"></span><span id="DDK_KSNODETYPE_NOISE_SUPPRESS_KS"></span>


KSNODETYPE\_干扰\_禁止节点表示的干扰抑制 (NS) 控件。 NS 节点具有一个输入的流和一个输出流的连接。 这两个流具有相同的格式。

当创建筛选器包含 NS 节点或节点重置时，节点最初配置为在直通模式下操作。

NS 节点可以合并到一个 AEC （回声抵消） 筛选器来支持完全双工 DirectSound 应用程序。 有关详细信息，请参阅[DirectSound 捕获效果](https://docs.microsoft.com/windows-hardware/drivers/audio/directsound-capture-effects)。

KSNODETYPE\_干扰\_AEC 筛选器中的取消节点应以启用硬件加速支持以下属性：

[**KSPROPERTY\_AUDIO\_CPU\_RESOURCES**](ksproperty-audio-cpu-resources.md)

[**KSPROPERTY\_音频\_算法\_实例**](ksproperty-audio-algorithm-instance.md)

[**KSPROPERTY\_TOPOLOGYNODE\_启用**](ksproperty-topologynode-enable.md)

[**KSPROPERTY\_TOPOLOGYNODE\_重置**](ksproperty-topologynode-reset.md)

KSPROPERTY\_TOPOLOGYNODE\_启用属性用于同时启用和禁用节点。 该节点禁用时，在直通模式下运行 （也就是说，它允许要传递到无需修改输出的输入的流）。

 

 





