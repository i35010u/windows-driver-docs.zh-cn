---
title: 从适配器取消绑定
description: 从适配器取消绑定
ms.assetid: cea2ce45-df0c-4c75-a780-5810ea01b987
keywords:
- 协议驱动程序 WDK 网络，取消绑定
- NDIS 协议驱动程序 WDK，取消绑定
- 从适配器 WDK 网络取消绑定
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fad4143ef0f7d18657ae4e94b03687738b01da3a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843018"
---
# <a name="unbinding-from-an-adapter"></a>从适配器取消绑定





NDIS 调用协议驱动程序的[*ProtocolUnbindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex)函数，以请求从基础适配器取消绑定驱动程序。 作为[*ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex)的倒数，NDIS 调用*ProtocolUnbindAdapterEx*来关闭到适配器的绑定，并释放驱动程序为绑定分配的资源。

在*ProtocolUnbindAdapterEx*中，协议驱动程序调用[**NdisCloseAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscloseadapterex)以关闭到基础适配器的绑定。 协议驱动程序将[**NdisOpenAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisopenadapterex)提供的句柄**NdisCloseAdapterEx**到其*NdisBindingHandle*参数。 此句柄标识 NDIS 应关闭的绑定。

协议驱动程序必须通过*ProtocolBindAdapterEx*函数或*ProtocolUnbindAdapterEx*函数关闭适配器。

如果协议驱动程序必须启动操作来关闭绑定，则驱动程序可以调用[**NdisUnbindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisunbindadapter)。 **NdisUnbindAdapter**计划一个工作项，该工作项导致 NDIS 调用*ProtocolUnbindAdapterEx*。 在对**NdisUnbindAdapter**的调用返回之前，此工作项可以运行。 因此，驱动程序编写器必须假定在**NdisUnbindAdapter**返回后绑定句柄无效。

如果协议驱动程序从*ProtocolUnbindAdapterEx*返回 NDIS\_状态\_"挂起"，则它必须调用具有最终状态的[**NdisCompleteUnbindAdapterEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompleteunbindadapterex)才能完成绑定请求。

如果 NDIS 从**NdisCloseAdapterEx**中返回 NDIS\_状态\_挂起，ndis 稍后会调用协议驱动程序的[*ProtocolCloseAdapterCompleteEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_close_adapter_complete_ex)函数。

如果绑定处于暂停状态，NDIS 可以调用*ProtocolUnbindAdapterEx* 。

所有解除绑定操作完成后，绑定将处于未绑定状态。

 

 





