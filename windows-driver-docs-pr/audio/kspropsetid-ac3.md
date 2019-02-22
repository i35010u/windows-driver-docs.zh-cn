---
title: KSPROPSETID\_AC3
description: KSPROPSETID\_AC3
ms.assetid: 172d8ed8-2dd3-438d-8dc6-f4f1bb128811
keywords:
- KSPROPSETID_AC3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29e14507ab50297e4e77f191c059239e9d250427
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522298"
---
# <a name="kspropsetidac3"></a>KSPROPSETID\_AC3


## <span id="ddk_kspropsetid_ac3_ks"></span><span id="DDK_KSPROPSETID_AC3_KS"></span>


`KSPROPSETID_AC3`属性集公开 ac-3 解码和编码的音频设备驱动程序的功能。

支持 ac-3 格式的音频驱动程序可以公开各种属性用于控制 ac-3 解码器/编码器的功能。 此外，可以查询的流属性来确定 AC-3 编码音频的特征。

当的音频硬件不支持特定功能时，该硬件的驱动程序应失败的 get 和 set 属性调用以通知上层驱动程序，它必须找到另一种方法来执行指定的函数。 例如，不支持动态范围压缩的解码器的驱动程序应失败这一功能的调用，以便为上层会知道它需要遵循 ac-3 解码器的流插入压缩程序。

有关 ac-3 压缩信息，请参阅在 ac-3 规范[Dolby Laboratories](https://go.microsoft.com/fwlink/p/?linkid=8730)网站。 标题为规范*数字音频压缩标准 (AC-3)*。

在此集中的属性项由 KSPROPERTY\_AC3 枚举值。

KSPROPSETID\_AC3 属性集包含以下属性：

[**KSPROPERTY\_AC3\_ALTERNATE\_AUDIO**](ksproperty-ac3-alternate-audio.md)

[**KSPROPERTY\_AC3\_BIT\_STREAM\_MODE**](ksproperty-ac3-bit-stream-mode.md)

[**KSPROPERTY\_AC3\_DIALOGUE\_LEVEL**](ksproperty-ac3-dialogue-level.md)

[**KSPROPERTY\_AC3\_DOWNMIX**](ksproperty-ac3-downmix.md)

[**KSPROPERTY\_AC3\_错误\_隐蔽**](ksproperty-ac3-error-concealment.md)

[**KSPROPERTY\_AC3\_LANGUAGE\_CODE**](ksproperty-ac3-language-code.md)

[**KSPROPERTY\_AC3\_ROOM\_TYPE**](ksproperty-ac3-room-type.md)

 

 





