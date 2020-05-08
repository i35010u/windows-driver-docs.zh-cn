---
title: KSPROPSETID\_e-ac3
description: KSPROPSETID\_e-ac3
ms.assetid: 172d8ed8-2dd3-438d-8dc6-f4f1bb128811
keywords:
- KSPROPSETID_AC3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ebf120c907b890d06b8747bb78578b280b42fc0c
ms.sourcegitcommit: 98930ca95b9adbb6e5e472f89e91ab084e67e31d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2020
ms.locfileid: "82925548"
---
# <a name="kspropsetid_ac3"></a>KSPROPSETID\_e-ac3


## <span id="ddk_kspropsetid_ac3_ks"></span><span id="DDK_KSPROPSETID_AC3_KS"></span>


`KSPROPSETID_AC3`属性集公开音频设备驱动程序的 AC 3 解码和编码功能。

支持 AC 3 格式的音频驱动程序可以公开多种属性，用于控制 AC 3 解码器/编码器的功能。 此外，还可以查询流的属性，以确定 AC 3 编码音频的特征。

当音频硬件不支持某个特定功能时，该硬件的驱动程序应使 get 和 set 属性调用失败，以通知上层驱动程序必须找到另一种执行指定功能的方法。 例如，如果解码器的驱动程序不支持动态范围压缩，则不支持动态范围压缩的驱动程序将无法调用此功能，因此，上层将知道需要在 AC 3 解码器后面的流中插入压缩程序。

有关 AC 3 压缩的信息，请参阅[杜比实验室](https://www.dolby.com/us/en/index.html)网站上的 ac'97 规范。 该规范标题为*数字音频压缩标准（AC-3）*。

此集中的属性项由 KSPROPERTY\_e-ac3 枚举值指定。

KSPROPSETID\_e-ac3 属性集包含以下属性：

[**KSPROPERTY\_E-ac3\_备用\_音频**](ksproperty-ac3-alternate-audio.md)

[**KSPROPERTY\_E-ac3\_位\_流\_模式**](ksproperty-ac3-bit-stream-mode.md)

[**KSPROPERTY\_E-ac3\_对话框\_级别**](ksproperty-ac3-dialogue-level.md)

[**KSPROPERTY\_e-ac3\_DOWNMIX**](ksproperty-ac3-downmix.md)

[**KSPROPERTY\_E-ac3\_错误\_CONCEALMENT**](ksproperty-ac3-error-concealment.md)

[**KSPROPERTY\_E-ac3\_语言\_代码**](ksproperty-ac3-language-code.md)

[**KSPROPERTY\_E-ac3\_房间\_类型**](ksproperty-ac3-room-type.md)

 

 





