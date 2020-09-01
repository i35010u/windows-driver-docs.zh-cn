---
title: 注册和打开地址系列
description: 注册和打开地址系列
ms.assetid: 2249adf9-2876-4442-be94-1a966d3f1c88
keywords:
- 地址系列 WDK 网络
- AFs WDK 网络
- 注册地址系列
- 打开地址系列
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5db77d3a82f3cbc151773729ee713bd19deda521
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212019"
---
# <a name="registering-and-opening-an-address-family"></a>注册和打开地址系列





呼叫管理器必须为其向面向连接的客户端提供呼叫管理器服务的每个 NIC 注册一个地址族。 同样，MCM 驱动程序必须为它所管理的 NIC 注册地址族。

注册地址族后，调用管理器或 MCM 驱动程序会使 NDIS 向绑定到该适配器的所有面向连接的客户端播发调用管理器或 MCM 驱动程序的服务。

如果面向连接的客户端可以使用由呼叫管理器或 MCM 驱动程序公布的服务，则它可以使用呼叫管理器或 MCM 驱动程序打开地址族。

### <a name="registering-an-address-family-from-a-call-manager"></a>从调用管理器注册地址族

[*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)函数将绑定到带有[**NdisOpenAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)的基础微型端口驱动程序后，调用管理器会调用[**NdisCmRegisterAddressFamilyEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex)来注册绑定的地址族 (参阅下图) 。

![说明如何使用呼叫管理器注册和打开地址族的示意图](images/cm-01.png)

对 **NdisCmRegisterAddressFamilyEx** 的调用会公布呼叫管理器的特定信号服务。 调用管理器必须在每次 *ProtocolBindAdapterEx* 函数和调用并成功绑定到带有 [**NdisOpenAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)的 NIC 时注册地址族。

呼叫管理器可以在它所绑定到的所有微型端口驱动程序中支持多个地址族。 呼叫管理器还可以在绑定到的单个 NIC 上支持多个地址族。 调用管理器必须为绑定上的每个地址族注册相同的入口点。 对于绑定到任何特定微型端口驱动程序的客户端，只有一个调用管理器可以支持特定类型的地址族。 有关注册呼叫管理器入口点的详细信息，请参阅 [CoNDIS Registration](condis-registration.md)。

### <a name="registering-an-address-family-from-an-mcm-driver"></a>从 MCM 驱动程序注册地址族

MCM 驱动程序在向[**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)注册其微型端口驱动程序入口点后从其[*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数调用**NdisMCmRegisterAddressFamilyEx** 。 有关 regsitering 入口点的详细信息，请参阅 [CoNDIS Registration](condis-registration.md)。 MCM 驱动程序调用 [**NdisMCmRegisterAddressFamilyEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmregisteraddressfamilyex) 一次，将其服务播发到面向连接的客户端 (参阅下图) 。

![演示如何使用 mcm 驱动程序注册和打开地址族的示意图](images/fig1-01.png)

具有板载连接的信号支持的 NIC 的微型端口驱动程序可以将自身注册为 MCM 驱动程序，即使可以使用呼叫管理器也是如此。 这样，此类 MCM 驱动程序抢先于调用管理器作为该 NIC 的呼叫管理器。

### <a name="opening-an-address-family"></a>打开地址族

调用管理器或 MCM 驱动程序对 **Ndis (M) CmRegisterAddressFamily** 的调用会使 ndis 调用绑定 (上每个面向连接的客户端的 [**ProtocolCoAfRegisterNotify**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_af_register_notify) 函数，如前面的两个图形) 所示。

*ProtocolCoAfRegisterNotify* 检查地址族数据，以确定客户端是否可以使用此特定 CM 或 MCM 驱动程序的服务。 客户端是否可以在 (M 中进行修改) CM 提供的地址族数据取决于呼叫管理器或 MCM 驱动程序的特定信号协议支持。

如果客户端发现提供的调用管理服务可接受， *ProtocolCoAfRegisterNotify* 将为客户端分配每个 AF 的上下文区域并调用 [**NdisClOpenAddressFamilyEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex)。 **NdisClOpenAddressFamilyEx** 不会将客户端的面向连接的入口点注册到 NDIS。 有关将面向连接的入口点注册到 NDIS 的详细信息，请参阅 [CoNDIS Registration](condis-registration.md)。

对 **NdisClOpenAddressFamilyEx** 的调用会使 NDIS 调用调用管理器或 MCM 驱动程序的 [**ProtocolCmOpenAf**](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_cm_open_af) 函数 (如之前) 的两个图形中所示。 *ProtocolCmOpenAf* 确保客户端传递到有效的地址族，并分配和初始化代表打开此地址族实例的客户端所需的资源。 *ProtocolCmOpenAf* 还存储 NDIS 提供的 *NdisAfHandle* ，表示呼叫管理器与打开地址系列的客户端之间的关联。

*ProtocolCmOpenAf* 可以同步或异步完成。 若要异步完成，调用管理器的 *ProtocolCmOpenAf* 函数将调用 [**NdisCmOpenAddressFamilyComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmopenaddressfamilycomplete);MCM 驱动程序的 *ProtocolCmOpenAf* 函数将调用 [**NdisMCmOpenAddressFamilyComplete**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmopenaddressfamilycomplete)。 调用**ndis (M) CmOpenAddressFamilyComplete**导致 ndis 调用最初称为**NdisClOpenAddressFamilyEx**的客户端的*ProtocolOpenAfComplete*函数。

如果客户端对 **NdisClOpenAddressFamilyEx** 的调用成功，NDIS 会将 *NdisAfHandle* 返回给客户端，表示呼叫管理器和客户端之间的关联。

如果客户端接受传入调用，则它通常会在其*ProtocolClOpenAfCompleteEx*函数中[注册一个或多个 sap](registering-a-sap.md) ，方法是在成功调用[**NdisClOpenAddressFamilyEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex)后调用[**NdisClRegisterSap**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclregistersap) 。

如果客户端发出传出呼叫，则它可以在其*ProtocolClOpenAfCompleteEx*函数中[创建一个或多个 VCs](creating-a-vc.md) ，以便通过一个或多个客户端发出传出呼叫的请求。

 

