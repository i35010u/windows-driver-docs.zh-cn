---
title: 创建 VC
description: 创建 VC
ms.assetid: 29d7f2b3-0514-46f8-8b12-02275b404a2a
keywords:
- 虚拟连接 WDK CoNDIS，创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 607ad68529c45328a6c01456e83ee9794f3b07d8
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835032"
---
# <a name="creating-a-vc"></a>创建 VC





发出传出呼叫之前，面向连接的客户端启动创建虚拟连接（VC）。 在指示对面向连接的客户端的传入调用之前，调用管理器或 MCM 驱动程序将启动 VC 的创建。 设置并激活 VC 后，可以在 VC 上传输或接收客户端数据。

调用管理器或 MCM 驱动程序还可以启动一个 VC，其中的信号消息与网络组件（如网络交换机）进行交换。

### <a name="client-initiated-creation-of-a-vc"></a>客户端启动的 VC 创建

在使用[**NdisClMakeCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclmakecall)[进行调用](making-a-call.md)之前，面向连接的客户端将调用[**NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc)来启动 VC 的创建。

下图显示了启动创建 VC 的呼叫管理器的客户端。

![说明开始创建 vc 的呼叫管理器客户端的关系图](images/cm-05.png)

下图显示了启动创建 VC 的 MCM 驱动程序的客户端。

![说明 mcm 驱动程序启动创建 vc 的客户端的关系图](images/fig1-05.png)

当呼叫管理器面向连接的客户端调用**NdisCoCreateVc**时，NDIS 会调用，作为同步操作、调用管理器的[**ProtocolCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_create_vc)函数和基础微型端口的[**MiniportCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_create_vc)函数驱动程序（请参阅本主题中的第一个图形）。 NDIS 将表示 VC 的*NdisVcHandle*传递到*ProtocolCoCreateVc*和*MiniportCoCreateVc*。 如果对**NdisCoCreateVc**的调用成功，NDIS 会将*NdisVcHandle*返回到**NdisCoCreateVc**。

*ProtocolCoCreateVc*分配和初始化调用管理器所需的任何动态资源和结构，以便在将激活的 VC 上执行后续操作。 *MiniportCoCreateVc*分配和初始化微型端口驱动程序所需的任何资源，以维护有关 VC 的状态信息。 *ProtocolCoCreateVc*和*MiniportCoCreateVc*都存储*NdisVcHandle* 。

当 MCM 驱动程序的面向连接的客户端时，对**NdisCoCreateVc**的调用会使 NDIS 调用 MCM 驱动程序的*ProtocolCoCreateVc*函数（请参阅客户端启动的 VC （MCM 驱动程序）创建）。 在这种情况下， *ProtocolCoCreateVc*将对 VC 执行所需的资源分配和初始化。 不会对*MiniportCoCreateVc*进行任何调用（内部或其他），因为 MCM 驱动程序未提供此类功能。

### <a name="call-manager-initiated-creation-of-a-vc"></a>调用管理器启动的 VC 创建

在使用[**NdisCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmdispatchincomingcall)指示对面向连接的客户端的[传入调用](indicating-an-incoming-call.md)之前，调用管理器会调用**NdisCoCreateVc** ，以启动 VC 的创建（见下图）。

![说明开始创建 vc 的调用管理器的关系图](images/cm-06.png)

当呼叫管理器调用[**NdisCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscocreatevc)时，NDIS 将调用，作为同步操作，注册了将接收调用的 SAP 的面向连接的客户端的[**ProtocolCoCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_create_vc)函数，[**以及**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_co_create_vc)基础微型端口的 MiniportCoCreateVc 函数。 NDIS 将表示 VC 的*NdisVcHandle*传递到*ProtocolCoCreateVc*和*MiniportCoCreateVc*。 如果对**NdisCoCreateVc**的调用成功，NDIS 会将*NdisVcHandle*返回到**NdisCoCreateVc**。

### <a name="mcm-driver-initiated-creation-of-a-vc"></a>MCM 驱动程序启动的 VC 创建

在使用[**NdisMCmDispatchIncomingCall**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmdispatchincomingcall)指示对面向连接的客户端的[传入调用](indicating-an-incoming-call.md)之前，MCM 驱动程序将调用[**NdisMCmCreateVc**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismcmcreatevc)以启动 VC 的创建（见下图）。

![阐释 mcm 驱动程序启动创建 vc 的关系图](images/fig1-06.png)

当 MCM 驱动程序调用**NdisMCmCreateVc**时，NDIS 在**NdisMCmCreateVc**返回之前调用，作为同步操作，[**该客户端将调用**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_co_create_vc)的 SAP 注册到收发. NDIS 将表示 VC 的*NdisVcHandle*传递到*ProtocolCoCreateVc*。 如果对**NdisMCmCreateVc**的调用成功，NDIS 会将*NdisVcHandle*返回到**NdisMCmCreateVc**。

*ProtocolCoCreateVc*分配和初始化客户端在 VC 上执行后续操作所需的所有动态资源和结构。 *ProtocolCoCreateVc*还存储*NdisVcHandle* 。

请注意，当 MCM 驱动程序创建 VC 以便与网络组件交换信号消息时，它不使用**Ndis * Xxx*** 调用来创建 vc。 事实上，MCM 驱动程序不使用**Ndis * Xxx*** 调用来创建、激活、停用或删除此类 VCs。 相反，MCM 驱动程序在内部执行这些操作。 因此，此类 VCs 对于 NDIS 是不透明的。

 

 





