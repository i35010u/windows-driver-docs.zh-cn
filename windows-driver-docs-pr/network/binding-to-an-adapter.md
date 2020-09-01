---
title: 绑定到适配器
description: 绑定到适配器
ms.assetid: 583b7c73-fbc7-4d25-95f7-973cede61ec8
keywords:
- 协议驱动程序 WDK 网络，绑定到适配器
- NDIS 协议驱动程序 WDK，绑定到适配器
- 绑定操作 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcd1e4bea67d025e1ca7abd3b58ef102ef87963a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89206475"
---
# <a name="binding-to-an-adapter"></a>绑定到适配器





只要驱动程序可以绑定到的基础适配器可用，NDIS 就会调用协议驱动程序的 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex) 函数来打开绑定。 在 NDIS 调用 *ProtocolBindAdapterEx*后，绑定进入 "正在打开" 状态。 在 *打开* 状态中，协议驱动程序为绑定分配资源并打开适配器。

NDIS 传递到 *ProtocolBindAdapterEx* 绑定操作的 NDIS 上下文，以及指向 [**ndis \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters) 结构的指针。 此结构包含有关适配器的信息，例如：

-   适配器的名称。

-   注册表中协议服务项下的特定于此绑定的参数的注册表位置。

-   适配器的物理设备对象。

若要打开适配器，协议驱动程序将调用 [**NdisOpenAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex) 函数。 协议驱动程序将以下内容传递给 **NdisOpenAdapterEx**：

-   NDIS 在**NdisRegisterProtocolDriver**函数的*NdisProtocolHandle*参数处返回给驱动程序的句柄。

-   此绑定的协议驱动程序上下文。

-   指向 [**NDIS \_ 开放式 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_open_parameters)类型的结构的指针。

[**NDIS \_"打开 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_open_parameters) " 包含 **NdisOpenAdapterEx** 应打开的适配器的名称、协议驱动程序支持的一组中等类型以及驱动程序可在此绑定上接收的帧类型的数组（可选）。

如果协议驱动程序 \_ 从 ProtocolBindAdapterEx 返回 NDIS 状态 \_ "挂起"，则它必须调用具有最终状态的[**NdisCompleteBindAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompletebindadapterex)才能完成绑定请求。 *ProtocolBindAdapterEx*

如果 NDIS \_ 从 NdisOpenAdapterEx 返回 ndis 状态 \_ "挂起"，则在完成打开请求后，ndis 会将协议驱动程序的[*ProtocolOpenAdapterCompleteEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_open_adapter_complete_ex)函数与最终状态一起调用。 **NdisOpenAdapterEx**

当驱动程序成功打开到适配器的绑定后，绑定处于暂停状态。

协议驱动程序调用 [**NdisCloseAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex) 函数来关闭适配器。 驱动程序可以从*ProtocolBindAdapterEx*函数或[*ProtocolUnbindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)函数调用**NdisCloseAdapterEx** 。

如果在打开适配器后和完成绑定请求之前发生了故障， *ProtocolBindAdapterEx* 会遇到故障，必须关闭对适配器的绑定，然后才能调用 **NdisCloseAdapterEx**。 有关关闭适配器的详细信息，请参阅 [从适配器解除绑定](unbinding-from-an-adapter.md)。

 

