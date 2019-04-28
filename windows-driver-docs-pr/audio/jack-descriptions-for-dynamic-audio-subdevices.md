---
title: 针对动态音频子设备的插孔说明
description: 针对动态音频子设备的插孔说明
ms.assetid: e04f4000-3b93-4f4b-afec-007e5821f125
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 071116f3e455f4d61e0653c0a986f1d3732aa908
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333452"
---
# <a name="jack-descriptions-for-dynamic-audio-subdevices"></a>针对动态音频子设备的插孔说明


在 Windows Vista 及更高版本， [ **KSPROPERTY\_JACK\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff537364)属性上子音频适配器中提供有关插孔信息或插孔的集合。 (在此上下文中，术语*子*是的同义词*KS 筛选器*。)属性值是一个或多个数组[ **KSJACK\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff537136)结构。 每个结构描述颜色、 连接器类型和 jack 的物理位置。 此外，该结构包含**IsConnected**成员**TRUE**如果音频终结点设备如麦克风或耳机插入的插孔，并且是**FALSE**jack 是否为空。 若要提供的最新值**IsConnected**，动态子适配器驱动程序依赖的音频硬件 jack 存在检测功能。 对于 （与没有 jack 存在检测），静态子**IsConnected**的成员应该始终**TRUE**。 有关详细信息，请参阅[Jack Description 属性](jack-description-property.md)。

当用户将即插即用上动态子插孔中时，适配器驱动程序应调用[ **PcRegisterSubdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff537731)函数以注册子。 虽然子仍为注册状态，如果适配器驱动程序将收到包含 KSPROPERTY IOCTL\_JACK\_驱动程序应设置为子请求说明**IsConnected**的成员属性值设置为 **，则返回 TRUE**。

当用户将即插即用删除从上动态子插孔时，适配器驱动程序应调用[ **IUnregisterSubdevice::UnregisterSubdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff537032)方法来删除子的注册。 虽然子未注册，如果适配器驱动程序将收到包含 KSPROPERTY IOCTL\_JACK\_驱动程序应设置为子请求说明**IsConnected**的成员属性值设置为**FALSE**。

 

 




