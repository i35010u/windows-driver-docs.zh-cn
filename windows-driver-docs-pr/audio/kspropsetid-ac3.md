---
title: KSPROPSETID \_ e-ac3
description: KSPROPSETID \_ e-ac3
keywords:
- KSPROPSETID_AC3
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f71c6496d739866a825fab38b43300ba3e45a347
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801125"
---
# <a name="kspropsetid_ac3"></a>KSPROPSETID \_ e-ac3


## <span id="ddk_kspropsetid_ac3_ks"></span><span id="DDK_KSPROPSETID_AC3_KS"></span>


`KSPROPSETID_AC3`属性集公开音频设备驱动程序的 AC 3 解码和编码功能。

支持 AC 3 格式的音频驱动程序可以公开多种属性，用于控制 AC 3 解码器/编码器的功能。 此外，还可以查询流的属性，以确定 AC 3 编码音频的特征。

当音频硬件不支持某个特定功能时，该硬件的驱动程序应使 get 和 set 属性调用失败，以通知上层驱动程序必须找到另一种执行指定功能的方法。 例如，如果解码器的驱动程序不支持动态范围压缩，则不支持动态范围压缩的驱动程序将无法调用此功能，因此，上层将知道需要在 AC 3 解码器后面的流中插入压缩程序。

有关 AC 3 压缩的信息，请参阅 [杜比实验室](https://www.dolby.com/us/en/index.html) 网站上的 ac'97 规范。 该规范标题为 *数字音频压缩标准 (AC-3)*。

此集中的属性项由 KSPROPERTY \_ e-ac3 枚举值指定。

KSPROPSETID \_ e-ac3 属性集包含以下属性：

[**KSPROPERTY \_ E-ac3 \_ 备用 \_ 音频**](ksproperty-ac3-alternate-audio.md)

[**KSPROPERTY \_ E-ac3 \_ 位 \_ 流 \_ 模式**](ksproperty-ac3-bit-stream-mode.md)

[**KSPROPERTY \_ E-ac3 \_ 对话框 \_ 级别**](ksproperty-ac3-dialogue-level.md)

[**KSPROPERTY \_ E-ac3 \_ DOWNMIX**](ksproperty-ac3-downmix.md)

[**KSPROPERTY \_ E-ac3 \_ 错误 \_ CONCEALMENT**](ksproperty-ac3-error-concealment.md)

[**KSPROPERTY \_ E-ac3 \_ 语言 \_ 代码**](ksproperty-ac3-language-code.md)

[**KSPROPERTY \_ E-ac3 \_ 房间 \_ 类型**](ksproperty-ac3-room-type.md)

 

 





