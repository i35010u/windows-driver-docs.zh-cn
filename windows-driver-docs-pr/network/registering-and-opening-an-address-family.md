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
ms.openlocfilehash: 07a20ebfb56bf93b080030a160c825baedfa86de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63364120"
---
# <a name="registering-and-opening-an-address-family"></a>注册和打开地址系列





呼叫管理器必须注册到面向连接的客户端在其提供调用管理器服务的每个 NIC 的地址族。 同样，MCM 驱动程序必须注册它所管理的 NIC 的地址族。

通过注册地址族，呼叫管理器或 MCM 驱动程序会导致 NDIS 要播发的呼叫管理器或 MCM 驱动程序的服务添加到所有面向连接的客户端都将绑定到适配器。

如果面向连接的客户端可以使用所播发的呼叫管理器或 MCM 驱动程序的服务，它可以与呼叫管理器或 MCM 驱动程序打开地址族。

### <a name="registering-an-address-family-from-a-call-manager"></a>注册地址族从呼叫管理器

后其[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)函数将绑定到与基础微型端口驱动程序[ **NdisOpenAdapterEx**](https://msdn.microsoft.com/library/windows/hardware/ff563715)，呼叫管理器调用[ **NdisCmRegisterAddressFamilyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff561685)注册地址族的绑定 （请参阅下图）。

![说明注册和使用呼叫管理器中打开地址族的关系图](images/cm-01.png)

在调用**NdisCmRegisterAddressFamilyEx**播发呼叫管理器的特定信号服务。 呼叫管理器必须注册一个地址系列每次时，其*ProtocolBindAdapterEx*函数和调用，并已成功将绑定到与 NIC [ **NdisOpenAdapterEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563715).

呼叫管理器可以支持跨所有微型端口驱动程序绑定到多个地址族。 呼叫管理器还可以在绑定到单个 NIC 上支持多个地址族。 呼叫管理器必须注册在绑定上每个地址族的同一个入口点。 只有一个呼叫管理器可以绑定到任何特定的微型端口驱动程序的客户端支持特定类型的地址族。 关于注册呼叫管理器入口点的详细信息，请参阅[CoNDIS 注册](condis-registration.md)。

### <a name="registering-an-address-family-from-an-mcm-driver"></a>注册地址族 MCM 驱动程序

MCM 驱动程序调用**NdisMCmRegisterAddressFamilyEx**从其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数之后，注册其使用的微型端口驱动程序入口点[**NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)。 详细了解 regsitering 入口点，请参阅， [CoNDIS 注册](condis-registration.md)。 MCM 驱动程序调用[ **NdisMCmRegisterAddressFamilyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff563554)一次用来播发其服务添加到面向连接的客户端 （请参阅下图）。

![说明注册和使用 mcm 驱动程序打开地址族的关系图](images/fig1-01.png)

已载入面向连接的信号的支持的 NIC 的微型端口驱动程序可以将自身注册为 MCM 驱动程序即使呼叫管理器可能可用。 通过此操作，此类的 MCM 驱动程序会抢占该 nic。 呼叫管理器作为呼叫管理器

### <a name="opening-an-address-family"></a>打开地址系列

呼叫管理器或 MCM 驱动程序调用**Ndis (M) CmRegisterAddressFamily** NDIS 调用将导致[ **ProtocolCoAfRegisterNotify** ](https://msdn.microsoft.com/library/windows/hardware/ff570251)的每个函数面向连接的客户端上的绑定 （如上面的两个图中所示）。

*ProtocolCoAfRegisterNotify*检查以确定客户端是否可以使用此特定的 CM 或 MCM 驱动程序的服务的地址族数据。 客户端是否可以进行修改 (M) CM 提供的地址族数据中依赖于特定的信号协议支持的呼叫管理器或 MCM 驱动程序。

如果客户端查找提供的调用管理服务可以接受的*ProtocolCoAfRegisterNotify*在客户端和调用分配的每个 AF 上下文区域[ **NdisClOpenAddressFamilyEx**](https://msdn.microsoft.com/library/windows/hardware/ff561639). **NdisClOpenAddressFamilyEx**不会使用 NDIS 注册客户端的面向连接的入口点。 使用 NDIS 注册面向连接的入口点相关的详细信息，请参阅[CoNDIS 注册](condis-registration.md)。

在调用**NdisClOpenAddressFamilyEx** NDIS 调用管理器的调用或 MCM 驱动程序将导致[ **ProtocolCmOpenAf** ](https://msdn.microsoft.com/library/windows/hardware/ff570249)函数 （如前面所示已在两个数字）。 *ProtocolCmOpenAf*可确保客户端传递有效的地址系列和分配并初始化代表正在打开此实例的地址族的客户端执行操作所需的资源。 *ProtocolCmOpenAf*还会将存储 NDIS 提供*NdisAfHandle*表示呼叫管理器和用于打开地址系列的客户端之间的关联。

*ProtocolCmOpenAf*可以同步或异步完成。 若要以异步方式完成*ProtocolCmOpenAf*呼叫管理器的函数调用[ **NdisCmOpenAddressFamilyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff561682); *ProtocolCmOpenAf* MCM 驱动程序的函数调用[ **NdisMCmOpenAddressFamilyComplete**](https://msdn.microsoft.com/library/windows/hardware/ff563552)。 在调用**Ndis (M) CmOpenAddressFamilyComplete** NDIS 调用将导致*ProtocolOpenAfComplete*的客户端的最初调用的函数**NdisClOpenAddressFamilyEx**.

如果客户端的调用**NdisClOpenAddressFamilyEx**是否成功，请返回到客户端的 NDIS *NdisAfHandle*表示呼叫管理器和客户端打开地址之间的关联系列。

如果客户端接受传入的调用，但通常[注册一个或多个 SAPs](registering-a-sap.md)从其*ProtocolClOpenAfCompleteEx*函数通过调用[ **NdisClRegisterSap**](https://msdn.microsoft.com/library/windows/hardware/ff561648)按照其成功调用[ **NdisClOpenAddressFamilyEx**](https://msdn.microsoft.com/library/windows/hardware/ff561639)。

如果客户端的传出呼叫，它无法[创建一个或多个 VCs](creating-a-vc.md)在其*ProtocolClOpenAfCompleteEx*函数为预期的请求由一个或多个其客户端能够发起传出呼叫。

 

 





