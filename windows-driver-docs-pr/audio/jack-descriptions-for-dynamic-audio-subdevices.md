---
title: 针对动态音频子设备的插孔说明
description: 针对动态音频子设备的插孔说明
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55f7763e4831228be5b238f7d46e0ad9df813b22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784705"
---
# <a name="jack-descriptions-for-dynamic-audio-subdevices"></a>针对动态音频子设备的插孔说明


在 Windows Vista 和更高版本中， [**KSPROPERTY \_ 插座 \_ DESCRIPTION**](./ksproperty-jack-description.md) 属性提供有关音频适配器中 subdevice 上的插孔或插孔集合的信息。  (在此上下文中，术语 " *subdevice* " 与 *KS 筛选器* 同义。 ) 属性值是一个或多个 [**KSJACK \_ 说明**](./ksjack-description.md) 结构的数组。 每个结构都描述了插孔的颜色、连接符类型和物理位置。 此外，该结构还包含一个 **connectionmultiplexer.isconnected** 成员，如果使用麦克风或耳机等音频终结点设备插入插孔，则该成员为 **TRUE** ，如果插孔为空，则为 **FALSE** 。 若要为 **connectionmultiplexer.isconnected** 提供最新值，动态 subdevice 的适配器驱动程序依赖于音频硬件的插孔状态检测功能。 对于静态 subdevice (没有插孔状态检测) ， **connectionmultiplexer.isconnected** 成员应始终为 **TRUE**。 有关详细信息，请参阅 [插座说明属性](jack-description-property.md)。

当用户在动态 subdevice 上插入插孔时，适配器驱动程序应调用 [**PcRegisterSubdevice**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice) 函数来注册 subdevice。 尽管 subdevice 保持注册，但如果适配器驱动程序收到包含 subdevice 的 KSPROPERTY \_ 插座说明请求的 IOCTL， \_ 驱动程序应将属性值的 **connectionmultiplexer.isconnected** 成员设置为 **TRUE**。

当用户从动态 subdevice 的插孔中删除插头时，适配器驱动程序应调用 [**IUnregisterSubdevice：： UnregisterSubdevice**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregistersubdevice-unregistersubdevice) 方法，以删除 subdevice 的注册。 当 subdevice 未注册时，如果适配器驱动程序收到包含 subdevice 的 KSPROPERTY \_ 插座 \_ 说明请求的 IOCTL，则驱动程序应将属性值的 **connectionmultiplexer.isconnected** 成员设置为 **FALSE**。

 

