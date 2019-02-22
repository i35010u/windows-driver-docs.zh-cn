---
title: 音频的终结点，容器 ID
description: 音频的终结点容器 ID 本主题将讨论可靠的方式可用来获取与蓝牙音频设备关联的音频终结点的容器 ID。
ms.assetid: 82A852FF-688C-496A-AFF1-C68B0CC1756A
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2bfd7d30c0922b17748306f16b6eddabf9d1553f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556071"
---
# <a name="audio-endpoint-container-id"></a>音频的终结点，容器 ID


音频的终结点容器 ID 本主题将讨论可靠的方式可用来获取与蓝牙音频设备关联的音频终结点的容器 ID。

音频的终结点生成器使用枚举算法来确定容器的音频终结点的 Id，然后将这些 Id 存储为 MMDEVAPI 终结点属性存储中的属性。 在某些情况下，终结点生成器使用的逻辑不充足，可以应对蓝牙 I2S 设计音频终结点公开的音频驱动程序的容器 ID 由另一个枚举器的蓝牙枚举器。

涉及的 Bluetooth I2S 设计，使用其自己的蓝牙枚举此种情况很少见。 但无论如何，您可以开发音频驱动程序以便为此类方案提供支持。 在这种情况下，音频驱动程序的终结点可以支持新的容器 ID 属性。 新的属性[ **KSPROPERTY\_JACK\_CONTAINERID** ](https://msdn.microsoft.com/library/windows/hardware/dn265129)并且已添加到现有[KSPROPSETID\_Jack](https://msdn.microsoft.com/library/windows/hardware/ff537484)设置属性。 值为 GUID，它是容器 id。 的数据类型

音频驱动程序支持**KSPROPERTY\_JACK\_CONTAINERID**，当且仅当，它可以可靠地获取正确的容器 ID 通过其他方式;例如，从蓝牙枚举器。

如果音频驱动程序支持**KSPROPERTY\_JACK\_CONTAINERID**属性，音频系统读取此属性的值从驱动程序，然后存储的值作为容器 ID 设置为音频终结点。

有关容器 Id 以及在上一部分中所述的算法的详细信息，请参阅[容器 ID](https://msdn.microsoft.com/library/windows/hardware/ff540024.aspx)并[音频终结点生成器算法](audio-endpoint-builder-algorithm.md)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题
[理论上的操作](theory-of-operation.md)  



