---
title: 创建 VC
description: 创建 VC
ms.assetid: 29d7f2b3-0514-46f8-8b12-02275b404a2a
keywords:
- 虚拟连接 WDK 的 CoNDIS，创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f6728dc8c803c5567f7dcc771331838322efb05
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357396"
---
# <a name="creating-a-vc"></a>创建 VC





在之前的传出调用，面向连接的客户端 (VC) 的虚拟连接启动的创建。 之前，该值指示对面向连接的客户端的传入呼叫，呼叫管理器或 MCM 驱动程序启动的 VC 的创建。 设置 VC 并将其激活后，可以传输或接收 VC 上客户端数据。

呼叫管理器或 MCM 驱动程序还可启动的信号消息进行交换网络组件，例如网络交换机的 VC 创建。

### <a name="client-initiated-creation-of-a-vc"></a>客户端发起的 VC 的创建

之前[拨打电话](making-a-call.md)与[ **NdisClMakeCall**](https://msdn.microsoft.com/library/windows/hardware/ff561635)，在面向连接的客户端调用[ **NdisCoCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff561696)若要启动的 VC 创建。

下图显示的某调用的客户端管理器启动 VC 创建。

![说明启动 vc 创建呼叫管理器的客户端的关系图](images/cm-05.png)

下图显示了启动 VC 创建 MCM 驱动程序的客户端。

![说明启动 vc 创建 mcm 驱动程序的客户端的关系图](images/fig1-05.png)

当呼叫管理器的面向连接的客户端调用**NdisCoCreateVc**，NDIS 调用，以与同步操作[ **ProtocolCoCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff570252)调用的函数管理器和[ **MiniportCoCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff559354)基础微型端口驱动程序的函数 （请参阅本主题中的第一个图形）。 NDIS 传递*NdisVcHandle*同时表示 VC *ProtocolCoCreateVc*并*MiniportCoCreateVc*。 如果在调用**NdisCoCreateVc**是否成功，请返回 NDIS *NdisVcHandle*到**NdisCoCreateVc**。

*ProtocolCoCreateVc*分配并初始化任何动态资源和呼叫管理器需要执行后续操作将激活 VC 的结构。 *MiniportCoCreateVc*分配并初始化微型端口驱动程序所需的用于维护有关 VC 的状态信息的任何资源。 这两*ProtocolCoCreateVc*并*MiniportCoCreateVc*存储*NdisVcHandle* 。

当 MCM 驱动程序，对的调用的面向连接的客户端**NdisCoCreateVc** NDIS 调用 MCM 驱动程序将导致*ProtocolCoCreateVc*函数 （请参见 Client-Initiated VC （MCM 驱动程序创建存在））。 在这种情况下， *ProtocolCoCreateVc*为 VC 执行必要的分配和资源的初始化。 到没有调用 （内部或其他方式） *MiniportCoCreateVc*，这是因为 MCM 驱动程序不提供此类函数。

### <a name="call-manager-initiated-creation-of-a-vc"></a>调用管理器启动创建 VC

之前[，该值指示的传入呼叫](indicating-an-incoming-call.md)向面向连接的客户端与[ **NdisCmDispatchIncomingCall**](https://msdn.microsoft.com/library/windows/hardware/ff561664)，呼叫管理器调用**NdisCoCreateVc**若要启动的 VC 创建 （请参阅下图）。

![说明启动 vc 创建呼叫管理器的关系图](images/cm-06.png)

当呼叫管理器调用[ **NdisCoCreateVc**](https://msdn.microsoft.com/library/windows/hardware/ff561696)，NDIS 调用，以与同步操作[ **ProtocolCoCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff570252)的函数面向连接的客户端注册 SAP 在其正在接收调用，并将[ **MiniportCoCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff559354)函数的基础的微型端口。 NDIS 传递*NdisVcHandle*同时表示 VC *ProtocolCoCreateVc*并*MiniportCoCreateVc*。 如果在调用**NdisCoCreateVc**是否成功，请返回 NDIS *NdisVcHandle*到**NdisCoCreateVc**。

### <a name="mcm-driver-initiated-creation-of-a-vc"></a>MCM 驱动程序启动创建的 VC

之前[，该值指示的传入呼叫](indicating-an-incoming-call.md)向面向连接的客户端与[ **NdisMCmDispatchIncomingCall**](https://msdn.microsoft.com/library/windows/hardware/ff562830)，MCM 驱动程序调用[ **NdisMCmCreateVc** ](https://msdn.microsoft.com/library/windows/hardware/ff562812)若要启动的 VC 创建 （请参阅下图）。

![说明启动 vc 创建 mcm 驱动程序的关系图](images/fig1-06.png)

当 MCM 驱动程序调用**NdisMCmCreateVc**，作为一项同步操作之前的 NDIS 调用**NdisMCmCreateVc**返回时， [ **ProtocolCoCreateVc**](https://msdn.microsoft.com/library/windows/hardware/ff570252)的面向连接的客户端的注册的 SAP 接收调用的函数。 将传递 NDIS *NdisVcHandle* ，表示为 VC *ProtocolCoCreateVc*。 如果在调用**NdisMCmCreateVc**是否成功，请返回 NDIS *NdisVcHandle*到**NdisMCmCreateVc**。

*ProtocolCoCreateVc*分配并初始化任何动态资源和客户端需要执行后续操作 VC 的结构。 *ProtocolCoCreateVc*还会将存储*NdisVcHandle* 。

请注意，当 MCM 驱动程序创建 VC 时与网络组件的信号消息交换，它不使用**Ndis * Xxx*** 创建 VC 的调用。 事实上，MCM 驱动程序不使用**Ndis * Xxx*** 调用要创建，请激活、 停用，或删除此类 VCs。 相反，MCM 驱动程序将在内部执行这些操作。 因此，这种 VCs 是不透明的 NDIS。

 

 





