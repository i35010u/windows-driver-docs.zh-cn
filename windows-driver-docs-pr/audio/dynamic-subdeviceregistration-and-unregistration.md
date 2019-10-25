---
title: 动态子设备注册和注销
description: 动态子设备注册和注销
ms.assetid: 7157b7b3-655b-49d9-be45-c4a86a3cc82d
keywords:
- 动态 subdevice WDK 音频
- 音频 subdevices WDK
- 注册音频 subdevices WDK
- 注销音频 subdevices WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 870eda232a86e7316b008a3e14a52980d8a80802
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831254"
---
# <a name="dynamic-subdevice-registration-and-unregistration"></a>动态子设备注册和注销


支持某种形式的插孔状态检测的设备称为动态设备，其插孔必须支持[**KSPROPERTY\_插孔\_DESCRIPTION**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-description)属性。 以下步骤显示动态设备的驱动程序为这些动态设备创建、注册或注销关联的 subdevices 时所使用的算法。 Subdevices 以筛选器的形式创建。

以下步骤显示了在加载音频设备驱动程序时音频设备插入插孔后会发生什么情况：

1.  驱动程序使用插孔存在检测来确定是否有设备插入插孔。 驱动程序调用[**PcRegisterSubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice) ，以使用[Portcls](introduction-to-port-class.md)注册拓扑筛选器。 拓扑筛选器注册后，将创建一个[**KSCATEGORY\_音频**](https://docs.microsoft.com/windows-hardware/drivers/install/kscategory-audio)接口。

2.  当创建了**KSCATEGORY\_音频**接口并且[AudioEndpoint 生成器](audio-endpoint-builder-algorithm.md)创建并初始化了关联的终结点，然后将其状态设置为 "活动" 时，将通知音频堆栈。

3.  驱动程序将向 Portcls 注册一个波形滤镜，并通知音频堆栈。

4.  驱动程序调用[**PcRegisterPhysicalConnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregisterphysicalconnection) ，以将波形筛选器与拓扑筛选器连接。 然后，将此物理连接注册到 Portcls。

5.  驱动程序将[**KSJACK\_描述**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description)结构的 connectionmultiplexer.isconnected 成员设置为**TRUE** ，以指示有一个设备插入插孔。

**注意**   如果音频设备缺少插孔存在检测，则**connectionmultiplexer.isconnected**成员必须始终为**TRUE**。 若要确认设备是否支持插孔状态检测，客户端应用程序可以调用[IKsJackDescription2：： GetJackDescription2](https://go.microsoft.com/fwlink/p/?linkid=143698)来读取[**KSJACK\_DESCRIPTION2**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksjack-description2)结构的 JackCapabilities 标志。 如果此标志具有 JACKDESC2\_存在\_检测\_功能位，则表明终结点支持插孔存在检测。 在这种情况下，可以将**connectionmultiplexer.isconnected**成员的返回值解释为插孔插入状态的准确反射。

 

以下步骤说明了在加载驱动程序的情况下，如果没有音频设备插入插孔，会发生什么情况：

1.  驱动程序使用插孔存在检测来确定没有设备插入插孔。 但它为插座注册了 Portcls 的拓扑筛选器，并创建了**KSCATEGORY\_音频**接口。

2.  创建**KSCATEGORY\_音频**接口时，将通知音频堆栈。 AudioEndpointBuilder 将从**KSJACK\_说明**属性中查询微型端口驱动程序以确定是否将终结点的状态设置为 "已拔下"。

3.  驱动程序将**KSJACK\_描述**结构的**connectionmultiplexer.isconnected**成员设置为**FALSE** ，以指示没有设备插入插孔。

有关音频终结点的不同状态的详细信息，请参阅[音频终结点生成器算法](audio-endpoint-builder-algorithm.md)。

为了满足前面对 subdevice 注册和注销过程的说明，支持插孔状态检测的设备驱动程序必须按以下方式进行响应，以响应插入和删除操作：

**设备驱动程序对插入插入的响应**

1.  驱动程序必须调用**PcRegisterSubdevice** ，以使用 Portcls 注册波形筛选器。
    **请注意**   在加载驱动程序时，驱动程序已在拓扑过滤器上调用了**PcRegisterSubdevice** ，但未将设备插入插孔。

     

2.  驱动程序必须调用**PcRegisterPhysicalConnection**来注册与 Portcls 的 "波形与拓扑筛选器" 连接。

3.  驱动程序必须将 **\_KSJACK**的**connectionmultiplexer.isconnected**成员设置为**TRUE**。

**插入删除的设备驱动程序响应**

1.  驱动程序必须调用[**IUnregisterPhysicalConnection：： UnregisterPhysicalConnection**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregisterphysicalconnection-unregisterphysicalconnection)以撤消波形筛选器与拓扑筛选器之间的物理连接。

2.  驱动程序必须调用[**IUnregisterSubdevice：： UnregisterSubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-iunregistersubdevice-unregistersubdevice)以撤消波形筛选器。

3.  驱动程序必须设置**KSJACK\_说明**结构**为 FALSE**的**connectionmultiplexer.isconnected**成员。

 

 




