---
title: CoNDIS TAPI 注册
description: CoNDIS TAPI 注册
ms.assetid: 656be990-9392-4e8b-ac4a-73e38b75c109
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 联网，TAPI 服务
- WDK WAN 台电话服务注册
- 连接网络、 注册的 CoNDIS TAPI WDK
- 注册的 CoNDIS TAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 258f22b57952a364035fc68c37e5c081fa24e6ca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366760"
---
# <a name="condis-tapi-registration"></a>CoNDIS TAPI 注册





本部分讨论如何 CoNDIS WAN 的微型端口驱动程序表明它支持 TAPI 服务和它设置 NDISWAN 和 NDPROXY 驱动程序的特定于 TAPI 的通信。

CoNDIS WAN 的微型端口驱动程序具有一个或多个 nic 注册其微型端口驱动程序入口点后，以下操作会导致 NDISWAN 和 NDPROXY 驱动程序相关联，以特定于 TAPI 的方式，与这些 Nic。

-   CoNDIS WAN 的微型端口驱动程序调用[ **NdisMCmRegisterAddressFamilyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563554)函数中的其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数来注册其调用管理器入口点和地址系列类型共同\_地址\_系列\_TAPI\_代理。 通过此操作，微型端口驱动程序播发，它提供了 TAPI 服务。

-   NDIS 调用 NDPROXY 的[ **ProtocolCoAfRegisterNotify** ](https://msdn.microsoft.com/library/windows/hardware/ff570251)函数，以通知 NDPROXY 新注册的地址族。 NDPROXY 的*ProtocolCoAfRegisterNotify*检查地址系列的数据，并确定它可以使用已集成到 WAN 的 CoNDIS 微型端口驱动程序的调用管理器提供的 TAPI 服务。 TAPI 支持的 CoNDIS WAN 的微型端口驱动程序是集成的微型端口调用管理器 (MCM) 驱动程序。

-   NDPROXY 调用[ **NdisClOpenAddressFamilyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561639)函数以打开与 WAN 的 CoNDIS 微型端口驱动程序相关联的 TAPI 代理地址族。 **NdisClOpenAddressFamilyEx**注册 NDIS NDPROXY 的面向连接的入口点。 这些入口点用于与 TAPI 支持的 CoNDIS WAN 的微型端口驱动程序进行通信。

-   NDPROXY 调用[ **NdisCmRegisterAddressFamilyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561685)来注册其调用管理器入口点和地址系列类型共同\_地址\_系列\_TAPI。 通过此操作，NDPROXY 公布它实现了 TAPI 服务。

-   NDIS 调用 NDISWAN 的*ProtocolCoAfRegisterNotify*函数，以通知 NDISWAN 新注册的地址族。 NDISWAN 的*ProtocolCoAfRegisterNotify*检查地址系列的数据，并确定 NDISWAN 可以使用 NDPROXY 提供的 TAPI 服务。

-   NDISWAN 调用**NdisClOpenAddressFamilyEx**函数以打开与 NDPROXY 相关联的 TAPI 地址族。 **NdisClOpenAddressFamilyEx**注册 NDIS NDISWAN 的面向连接的入口点。 这些入口点用于与 NDPROXY 通信。

-   NDISWAN 调用[ **NdisClRegisterSap** ](https://msdn.microsoft.com/library/windows/hardware/ff561648)函数来通知 NDPROXY NDISWAN 可以接受传入的调用上特定服务访问点 (SAP)。 在此调用，传递 NDISWAN [**共同\_SAP** ](https://msdn.microsoft.com/library/windows/hardware/ff545392)介绍 SAP 的结构。 NDISWAN 集**SapType**成员产生的 CO\_SAP 再到 AF\_TAPI\_SAP\_类型，以指定，SAP 用于 TAPI 调用。 NDISWAN 集**Sap**成员产生的 CO\_SAP 再到特定的 TAPI 设备类的字符串。 TAPI 应用程序提供了此字符串，当应用程序调用 TAPI **lineGetID**函数。 NDPROXY 应该通知 NDISWAN 发送到 SAP 的所有传入调用的。

 

 





