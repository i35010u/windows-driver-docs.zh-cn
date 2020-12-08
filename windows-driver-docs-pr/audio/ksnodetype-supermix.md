---
title: KSNODETYPE \_ SUPERMIX
description: KSNODETYPE \_ SUPERMIX
keywords:
- KSNODETYPE_SUPERMIX 音频设备
topic_type:
- apiref
api_name:
- KSNODETYPE_SUPERMIX
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f66bcbeafe84ab88fd0a913247606f2f2c3177cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799115"
---
# <a name="ksnodetype_supermix"></a>KSNODETYPE \_ SUPERMIX


## <span id="ddk_ksnodetype_supermix_ks"></span><span id="DDK_KSNODETYPE_SUPERMIX_KS"></span>


KSNODETYPE \_ SUPERMIX 节点表示 supermixer。 Supermixer 有一个输入流，其中包含 *m* 通道和一个包含 *n* 通道的输出流。 对于每个输出通道，supermixer 为添加到输出通道中的组合的每个输入通道指定组合级别。 *M* 通道输入流为 upmixed 或 down 到 *n* 通道。

KSNODETYPE \_ SUPERMIX 节点应支持以下必需属性：

[**KSPROPERTY \_ AUDIO \_ 混音 \_ 级 \_ 表**](ksproperty-audio-mix-level-table.md)

[**KSPROPERTY \_ 音频 \_ 混合 \_ 电平 \_**](ksproperty-audio-mix-level-caps.md)

 

 





