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
ms.openlocfilehash: 110894c3013f9c2bb81ea01fe77ac75c91c81c2f
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209797"
---
# <a name="condis-tapi-registration"></a>CoNDIS TAPI 注册





本部分讨论了 CoNDIS WAN 微型端口驱动程序如何指示它支持 TAPI 服务，以及如何使用 NDISWAN 和 NDPROXY 驱动程序设置特定于 TAPI 的通信。

CoNDIS WAN 微型端口驱动程序为一个或多个 Nic 注册了其微型端口驱动程序入口点后，以下操作将导致 NDISWAN 和 NDPROXY 驱动程序以特定于 TAPI 的方式与这些 Nic 关联。

-   CoNDIS WAN 微型端口驱动程序从其[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数内调用[**NdisMCmRegisterAddressFamilyEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregisteraddressfamilyex)函数，以注册其调用管理器入口点和地址族类型的 CO \_ 址 \_ 系列 \_ TAPI \_ 代理。 这样，微型端口驱动程序就会公布它提供 TAPI 服务。

-   NDIS 调用 NDPROXY 的 [**ProtocolCoAfRegisterNotify**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_af_register_notify) 函数来通知 NDPROXY 新注册的地址族。 NDPROXY 的 *ProtocolCoAfRegisterNotify* 检查地址系列数据，并确定它可以使用集成到 CoNDIS WAN 微型端口驱动程序中的呼叫管理器提供的 TAPI 服务。 支持 TAPI 的 CoNDIS WAN 微型端口驱动程序是集成的微型端口调用管理器 (MCM) 驱动程序。

-   NDPROXY 调用 [**NdisClOpenAddressFamilyEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex) 函数来打开与 CoNDIS WAN 微型端口驱动程序相关联的 TAPI 代理地址系列。 **NdisClOpenAddressFamilyEx** 用 NDIS 注册 NDPROXY 的面向连接的入口点。 这些入口点用于与支持 TAPI 的 CoNDIS WAN 微型端口驱动程序通信。

-   NDPROXY 调用 [**NdisCmRegisterAddressFamilyEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex) 来注册其呼叫管理器入口点和地址系列类型的 CO \_ 址 \_ 系列 \_ TAPI。 这样，NDPROXY 就会公布它实现了 TAPI 服务。

-   NDIS 调用 NDISWAN 的 *ProtocolCoAfRegisterNotify* 函数来通知 NDISWAN 新注册的地址族。 NDISWAN 的 *ProtocolCoAfRegisterNotify* 检查地址系列数据，并确定 NDISWAN 可以使用 NDPROXY 提供的 TAPI 服务。

-   NDISWAN 调用 **NdisClOpenAddressFamilyEx** 函数来打开与 NDPROXY 关联的 TAPI 地址系列。 **NdisClOpenAddressFamilyEx** 用 NDIS 注册 NDISWAN 的面向连接的入口点。 这些入口点用于与 NDPROXY 通信。

-   NDISWAN 调用 [**NdisClRegisterSap**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap) 函数来通知 NDPROXY，NDISWAN 可以在特定服务访问点 (SAP) 上接受传入呼叫。 在此调用中，NDISWAN 将传递描述 SAP 的 [**共同 \_ sap**](/previous-versions/windows/hardware/network/ff545392(v=vs.85)) 结构。 NDISWAN 将共同 SAP 的 **SapType** 成员设置为 \_ AF \_ tapi \_ SAP \_ 类型，以指定将 SAP 用于 TAPI 呼叫。 NDISWAN 将共同 sap 的 **sap** 成员设置为 \_ 特定 TAPI 设备类的字符串。 当应用程序调用 TAPI **lineGetID** 函数时，TAPI 应用程序会提供此字符串。 NDPROXY 应通知 NDISWAN 有关发送到 SAP 的所有传入呼叫。

 

