---
title: KSNODETYPE\_SUPERMIX
description: KSNODETYPE\_SUPERMIX
ms.assetid: fae4d315-b599-4226-8f1d-e1757320afb2
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
ms.openlocfilehash: a8e3f390c24573021f12367d53711b613e7ce359
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525562"
---
# <a name="ksnodetypesupermix"></a>KSNODETYPE\_SUPERMIX


## <span id="ddk_ksnodetype_supermix_ks"></span><span id="DDK_KSNODETYPE_SUPERMIX_KS"></span>


KSNODETYPE\_SUPERMIX 节点表示 supermixer。 Supermixer 已具有一个输入的流*m*通道和一个输出流，用*n*通道。 对于每个输出通道，supermixer 指定混级别为每个添加到输出通道中组合的输入通道。 *M*-通道的输入的流是 upmixed 或向下混合到*n*通道。

KSNODETYPE\_SUPERMIX 节点应支持以下必需的属性：

[**KSPROPERTY\_AUDIO\_MIX\_LEVEL\_TABLE**](ksproperty-audio-mix-level-table.md)

[**KSPROPERTY\_AUDIO\_MIX\_LEVEL\_CAPS**](ksproperty-audio-mix-level-caps.md)

 

 





