---
title: 针对动态音频子设备的插孔说明
description: 针对动态音频子设备的插孔说明
ms.assetid: e04f4000-3b93-4f4b-afec-007e5821f125
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b7cfbfc4dbbd85a324181367d582ca5c0e84965f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833193"
---
# <a name="jack-descriptions-for-dynamic-audio-subdevices"></a>针对动态音频子设备的插孔说明


在 Windows Vista 和更高版本中， [**KSPROPERTY\_插孔\_DESCRIPTION**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-description)属性提供有关在音频适配器上的 subdevice 上的插孔或插孔集合的信息。 （在此上下文中，术语 " *subdevice* " 与*KS 筛选器*同义。）属性值是一个或多个[**KSJACK\_说明**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description)结构的数组。 每个结构都描述了插孔的颜色、连接符类型和物理位置。 此外，该结构还包含一个**connectionmultiplexer.isconnected**成员，如果使用麦克风或耳机等音频终结点设备插入插孔，则该成员为**TRUE** ，如果插孔为空，则为**FALSE** 。 若要为**connectionmultiplexer.isconnected**提供最新值，动态 subdevice 的适配器驱动程序依赖于音频硬件的插孔状态检测功能。 对于静态 subdevice （无插孔状态检测）， **connectionmultiplexer.isconnected**成员应始终为**TRUE**。 有关详细信息，请参阅[插座说明属性](jack-description-property.md)。

当用户在动态 subdevice 上插入插孔时，适配器驱动程序应调用[**PcRegisterSubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)函数来注册 subdevice。 尽管 subdevice 保持注册，但如果适配器驱动程序收到包含 subdevice 的 KSPROPERTY\_插孔\_描述请求的 IOCTL，则驱动程序应将属性值的**connectionmultiplexer.isconnected**成员设置为**TRUE**.

当用户从动态 subdevice 的插孔中删除插头时，适配器驱动程序应调用[**IUnregisterSubdevice：： UnregisterSubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregistersubdevice-unregistersubdevice)方法，以删除 subdevice 的注册。 在 subdevice 未注册的情况下，如果适配器驱动程序收到包含 subdevice 的 KSPROPERTY\_插孔\_描述请求的 IOCTL，则驱动程序应将属性值的**connectionmultiplexer.isconnected**成员设置为**FALSE**。

 

 




