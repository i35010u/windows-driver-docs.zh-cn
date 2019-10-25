---
title: CoNDIS TAPI 注册
description: CoNDIS TAPI 注册
ms.assetid: 656be990-9392-4e8b-ac4a-73e38b75c109
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，TAPI 服务
- telephonic services WDK WAN，注册
- CoNDIS TAPI WDK 网络，注册
- 注册 CoNDIS TAPI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a051edf66e6d3739c4963079ecfa4cb07e7b4f16
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838186"
---
# <a name="condis-tapi-registration"></a>CoNDIS TAPI 注册





本部分讨论了 CoNDIS WAN 微型端口驱动程序如何指示它支持 TAPI 服务，以及如何使用 NDISWAN 和 NDPROXY 驱动程序设置特定于 TAPI 的通信。

CoNDIS WAN 微型端口驱动程序为一个或多个 Nic 注册了其微型端口驱动程序入口点后，以下操作将导致 NDISWAN 和 NDPROXY 驱动程序以特定于 TAPI 的方式与这些 Nic 关联。

-   CoNDIS WAN 微型端口驱动程序从其[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数内调用[**NdisMCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregisteraddressfamilyex)函数，以注册其调用管理器入口点和地址族类型 CO\_address\_系列\_TAPI\_代理。 这样，微型端口驱动程序就会公布它提供 TAPI 服务。

-   NDIS 调用 NDPROXY 的[**ProtocolCoAfRegisterNotify**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_af_register_notify)函数来通知 NDPROXY 新注册的地址族。 NDPROXY 的*ProtocolCoAfRegisterNotify*检查地址系列数据，并确定它可以使用集成到 CoNDIS WAN 微型端口驱动程序中的呼叫管理器提供的 TAPI 服务。 支持 TAPI 的 CoNDIS WAN 微型端口驱动程序是一个集成微型端口调用管理器（MCM）驱动程序。

-   NDPROXY 调用[**NdisClOpenAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex)函数来打开与 CoNDIS WAN 微型端口驱动程序相关联的 TAPI 代理地址系列。 **NdisClOpenAddressFamilyEx**用 NDIS 注册 NDPROXY 的面向连接的入口点。 这些入口点用于与支持 TAPI 的 CoNDIS WAN 微型端口驱动程序通信。

-   NDPROXY 调用[**NdisCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex)来注册其呼叫管理器入口点和地址族类型 CO\_ADDRESS\_系列\_TAPI。 这样，NDPROXY 就会公布它实现了 TAPI 服务。

-   NDIS 调用 NDISWAN 的*ProtocolCoAfRegisterNotify*函数来通知 NDISWAN 新注册的地址族。 NDISWAN 的*ProtocolCoAfRegisterNotify*检查地址系列数据，并确定 NDISWAN 可以使用 NDPROXY 提供的 TAPI 服务。

-   NDISWAN 调用**NdisClOpenAddressFamilyEx**函数来打开与 NDPROXY 关联的 TAPI 地址系列。 **NdisClOpenAddressFamilyEx**用 NDIS 注册 NDISWAN 的面向连接的入口点。 这些入口点用于与 NDPROXY 通信。

-   NDISWAN 调用[**NdisClRegisterSap**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap)函数来通知 NDPROXY，NDISWAN 可以接受对特定服务访问点（SAP）的传入呼叫。 在此调用中，NDISWAN 将传递描述 SAP 的[**共同\_sap**](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff545392(v=vs.85))结构。 NDISWAN 将共同\_SAP 的**SapType**成员设置\_TAPI\_SAP\_类型，以指定将 SAP 用于 TAPI 呼叫。 NDISWAN 将共同\_SAP 的**sap**成员设置为特定 TAPI 设备类的字符串。 当应用程序调用 TAPI **lineGetID**函数时，TAPI 应用程序会提供此字符串。 NDPROXY 应通知 NDISWAN 有关发送到 SAP 的所有传入呼叫。

 

 





