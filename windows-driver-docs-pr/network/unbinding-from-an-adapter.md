---
title: 从适配器取消绑定
description: 从适配器取消绑定
keywords:
- 协议驱动程序 WDK 网络，取消绑定
- NDIS 协议驱动程序 WDK，取消绑定
- 从适配器 WDK 网络取消绑定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df9313046c2f9f5b653e92845555acadc56a0bf4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839425"
---
# <a name="unbinding-from-an-adapter"></a>从适配器取消绑定





NDIS 调用协议驱动程序的 [*ProtocolUnbindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex) 函数，以请求从基础适配器取消绑定驱动程序。 作为 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)的倒数，NDIS 调用 *ProtocolUnbindAdapterEx* 来关闭到适配器的绑定，并释放驱动程序为绑定分配的资源。

在 *ProtocolUnbindAdapterEx* 中，协议驱动程序调用 [**NdisCloseAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex) 以关闭到基础适配器的绑定。 协议驱动程序将 [**NdisOpenAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)提供的句柄 **NdisCloseAdapterEx** 到其 *NdisBindingHandle* 参数。 此句柄标识 NDIS 应关闭的绑定。

协议驱动程序必须通过 *ProtocolBindAdapterEx* 函数或 *ProtocolUnbindAdapterEx* 函数关闭适配器。

如果协议驱动程序必须启动操作来关闭绑定，则驱动程序可以调用 [**NdisUnbindAdapter**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisunbindadapter)。 **NdisUnbindAdapter** 计划一个工作项，该工作项导致 NDIS 调用 *ProtocolUnbindAdapterEx*。 在对 **NdisUnbindAdapter** 的调用返回之前，此工作项可以运行。 因此，驱动程序编写器必须假定在 **NdisUnbindAdapter** 返回后绑定句柄无效。

如果协议驱动程序 \_ 从 ProtocolUnbindAdapterEx 返回 NDIS 状态 \_ "挂起"，则它必须调用具有最终状态的 [**NdisCompleteUnbindAdapterEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompleteunbindadapterex)才能完成绑定请求。 *ProtocolUnbindAdapterEx*

如果 NDIS \_ 从 NdisCloseAdapterEx 返回 ndis 状态 \_ "挂起"，ndis 稍后会调用协议驱动程序的 [*ProtocolCloseAdapterCompleteEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_close_adapter_complete_ex)函数。 **NdisCloseAdapterEx**

如果绑定处于暂停状态，NDIS 可以调用 *ProtocolUnbindAdapterEx* 。

所有解除绑定操作完成后，绑定将处于未绑定状态。

 

