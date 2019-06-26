---
title: 绑定到适配器
description: 绑定到适配器
ms.assetid: 583b7c73-fbc7-4d25-95f7-973cede61ec8
keywords:
- 协议驱动程序 WDK 网络绑定到适配器
- NDIS 协议驱动程序 WDK，绑定到适配器
- 绑定操作 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e99891f580090206f9d745374a792cc5ef636e9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386356"
---
# <a name="binding-to-an-adapter"></a>绑定到适配器





NDIS 调用协议驱动程序[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数以打开一个绑定，只要该驱动程序可以绑定到的基础适配器变得可用。 在 NDIS 后调用*ProtocolBindAdapterEx*，绑定将进入打开状态。 在中*打开*状态下，协议驱动程序绑定分配资源，将打开该适配器。

NDIS 将传递给*ProtocolBindAdapterEx*绑定操作，以及指向指针的 NDIS 上下文[ **NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)结构。 此结构包含以下有关适配器的信息：

-   适配器的名称。

-   特定于此协议服务的注册表项下的绑定参数注册表位置。

-   该适配器的的物理设备对象。

若要打开一个适配器，协议驱动程序调用[ **NdisOpenAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)函数。 协议驱动程序将传递到以下**NdisOpenAdapterEx**:

-   NDIS 驱动程序在返回的句柄*NdisProtocolHandle*的参数**NdisRegisterProtocolDriver**函数。

-   此绑定的协议驱动程序的上下文。

-   指向类型的结构的指针[ **NDIS\_打开\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_open_parameters)。

[**NDIS\_打开\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_open_parameters)包含适配器的信息，例如名称， **NdisOpenAdapterEx**应打开，介质的数组类型的协议驱动程序支持和 （可选） 该驱动程序可以接收此绑定的帧类型的数组。

如果协议驱动程序返回 NDIS\_状态\_从 PENDING *ProtocolBindAdapterEx*，它必须调用[ **NdisCompleteBindAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscompletebindadapterex)若要完成绑定请求的最终状态。

如果 NDIS 返回 NDIS\_状态\_从 PENDING **NdisOpenAdapterEx**，NDIS 更高版本调用协议驱动程序[ *ProtocolOpenAdapterCompleteEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_open_adapter_complete_ex)函数中，打开请求完成后的最终状态。

驱动程序已成功打开绑定到适配器后，该绑定将处于已暂停状态。

协议驱动程序调用[ **NdisCloseAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)函数以关闭适配器。 该驱动程序可以调用**NdisCloseAdapterEx**从*ProtocolBindAdapterEx*函数或[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)函数。

如果打开适配器之后，则绑定请求，在完成前*ProtocolBindAdapterEx*在遇到失败，必须关闭绑定到适配器，它可以调用**NdisCloseAdapterEx**。 有关关闭适配器的详细信息，请参阅[取消绑定从适配器](unbinding-from-an-adapter.md)。

 

 





