---
title: 动态子设备注册和注销
description: 动态子设备注册和注销
ms.assetid: 7157b7b3-655b-49d9-be45-c4a86a3cc82d
keywords:
- 动态子 WDK 音频
- 音频子设备 WDK
- 注册音频子设备 WDK
- 取消音频子设备 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09d625ee56111367272c94f0575f21bb75df7e8e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63333816"
---
# <a name="dynamic-subdevice-registration-and-unregistration"></a>动态子设备注册和注销


支持某种形式的插孔在场检测的设备称为动态设备，并且必须支持其插孔[ **KSPROPERTY\_JACK\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff537364)属性。 以下步骤显示的动态设备驱动程序用来创建、 注册或注销这些动态设备相关联的子设备的算法。 筛选器的窗体中创建子设备。

以下步骤演示音频设备插入的插孔，加载音频设备驱动程序时，会发生什么情况：

1.  用于确定存在驱动程序使用 jack 在场检测是插入的插孔的设备。 驱动程序调用[ **PcRegisterSubdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff537731)注册具有的拓扑筛选器[Portcls](introduction-to-port-class.md)。 一个[ **KSCATEGORY\_音频**](https://msdn.microsoft.com/library/windows/hardware/ff548261)由于拓扑筛选器注册而创建的接口。

2.  音频堆栈会收到通知时**KSCATEGORY\_音频**创建接口并[AudioEndpoint 生成器](audio-endpoint-builder-algorithm.md)创建和初始化关联的终结点，并将其状态设置为处于活动状态。

3.  该驱动程序注册 Portcls 批筛选器和音频堆栈会收到通知。

4.  驱动程序调用[ **PcRegisterPhysicalConnection** ](https://msdn.microsoft.com/library/windows/hardware/ff537726)连接批筛选器与拓扑筛选器。 向 Portcls 然后注册此物理连接。

5.  该驱动程序设置的 IsConnected 成员[ **KSJACK\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff537136)结构**TRUE**以指示设备已插入插孔中。

**请注意**  如果音频设备缺少 jack 存在检测**IsConnected**成员必须始终为**TRUE**。 若要确认设备是否支持 jack 存在检测，客户端应用程序可以调用[IKsJackDescription2::GetJackDescription2](https://go.microsoft.com/fwlink/p/?linkid=143698)若要读取的 JackCapabilities 标志[ **KSJACK\_DESCRIPTION2** ](https://msdn.microsoft.com/library/windows/hardware/ff537138)结构。 如果此标志有 JACKDESC2\_是否存在\_检测\_功能位集，它指示终结点支持 jack 存在检测。 在这种情况下，返回值**IsConnected**成员可以解释为应用的插孔插入状态的准确映像。

 

以下步骤介绍会发生什么情况是否有任何音频设备插入的插孔，加载驱动程序：

1.  驱动程序使用 jack 在场检测用于确定有不设备插入到的插孔。 但它拓扑筛选器会向注册 Portcls 的插孔，和一个**KSCATEGORY\_音频**创建接口。

2.  音频堆栈会收到通知时**KSCATEGORY\_音频**创建接口。 AudioEndpointBuilder 查询微型端口驱动程序来确定从**KSJACK\_说明**属性是否将终结点的状态设置为拔出。

3.  驱动程序集**IsConnected**的成员**KSJACK\_说明**结构**FALSE**以指示不存在设备插入到的插孔。

有关音频终结点的不同状态的详细信息，请参阅[音频终结点生成器算法](audio-endpoint-builder-algorithm.md)。

若要符合上述子注册和注销过程的说明，支持 jack 在场检测设备驱动程序必须按以下方式，以响应插入插入和删除响应：

**即插即用插入的设备驱动程序响应**

1.  驱动程序必须调用**PcRegisterSubdevice**注册 Portcls 批筛选器。
    **请注意**  驱动程序已调用**PcRegisterSubdevice**拓扑筛选器与插入的插孔任何设备中加载的驱动程序时。

     

2.  该驱动程序必须调用**PcRegisterPhysicalConnection** Portcls 注册"波次向拓扑筛选器"连接。

3.  该驱动程序必须设置**IsConnected**的成员**KSJACK\_说明**结构**TRUE**。

**即插即用删除设备驱动程序响应**

1.  驱动程序必须调用[ **IUnregisterPhysicalConnection::UnregisterPhysicalConnection** ](https://msdn.microsoft.com/library/windows/hardware/ff537024)注销批筛选器和拓扑筛选器之间的物理连接。

2.  驱动程序必须调用[ **IUnregisterSubdevice::UnregisterSubdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff537032)注销批筛选器。

3.  驱动程序必须设置**IsConnected**的成员**KSJACK\_说明**结构**FALSE**。

 

 




