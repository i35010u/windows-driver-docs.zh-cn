---
title: 音频终结点容器 ID
description: 音频终结点容器 ID 主题讨论了可用于获取与蓝牙音频设备关联的音频终结点的容器 ID 的可靠方法。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ddfef2008240371e1788ade26fcb7631fcef94b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784995"
---
# <a name="audio-endpoint-container-id"></a>音频终结点容器 ID


音频终结点容器 ID 主题讨论了可用于获取与蓝牙音频设备关联的音频终结点的容器 ID 的可靠方法。

音频终结点生成器使用枚举算法来确定音频终结点的容器 Id，然后将这些 Id 存储为 MMDEVAPI 终结点属性存储中的属性。 在某些情况下，终结点生成器使用的逻辑不足以处理蓝牙 I2S 设计，其中音频驱动程序所公开的音频终结点的容器 ID 由其他枚举器-蓝牙枚举器决定。

此方案涉及到使用其自己的蓝牙枚举器的蓝牙 I2S 设计。 但无论如何，你都可以开发音频驱动程序以提供对此类方案的支持。 在这种情况下，你的音频驱动程序可以为终结点支持新的容器 ID 属性。 新属性为 [**KSPROPERTY \_ 插座 \_ CONTAINERID**](./ksproperty-jack-containerid.md) ，并已添加到现有的 [KSPROPSETID \_ 插座](./kspropsetid-jack.md) 属性集。 该值是一个 GUID，它是容器 ID 的数据类型。

音频驱动程序支持 **KSPROPERTY 的 \_ 插孔 \_ CONTAINERID**，如果且仅当使用时，它可以通过其他方式可靠地获取正确的容器 ID;例如，从蓝牙枚举器。

如果音频驱动程序支持 **KSPROPERTY \_ 插座 \_ CONTAINERID** 属性，则音频系统将从驱动程序中读取此属性的值，然后将该值存储为音频终结点的容器 ID。

有关容器 Id 和前面部分中提到的算法的详细信息，请参阅 [容器 id](../install/container-ids.md) 和 [音频终结点生成器算法](audio-endpoint-builder-algorithm.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[操作理论](theory-of-operation.md)
