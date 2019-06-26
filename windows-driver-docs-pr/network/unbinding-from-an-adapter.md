---
title: 从适配器取消绑定
description: 从适配器取消绑定
ms.assetid: cea2ce45-df0c-4c75-a780-5810ea01b987
keywords:
- 协议驱动程序 WDK 连接网络、 取消绑定
- NDIS 协议驱动程序 WDK、 正在取消绑定
- 正在取消绑定从适配器 WDK 网络连接
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b38447857a314dacbcb010d5e8d24873a615507
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355452"
---
# <a name="unbinding-from-an-adapter"></a>从适配器取消绑定





NDIS 调用协议驱动程序[ *ProtocolUnbindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_unbind_adapter_ex)函数请求从基础适配器取消绑定驱动程序。 作为的倒数[ *ProtocolBindAdapterEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)，NDIS 调用*ProtocolUnbindAdapterEx*以关闭与适配器绑定，并以释放资源的驱动程序分配绑定。

在中*ProtocolUnbindAdapterEx*，协议驱动程序调用[ **NdisCloseAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscloseadapterex)关闭到基础适配器的绑定。 协议驱动程序传递**NdisCloseAdapterEx**句柄的[ **NdisOpenAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisopenadapterex)提供在其*NdisBindingHandle*参数。 此句柄标识的绑定的 NDIS 应关闭。

协议驱动程序必须关闭从适配器*ProtocolBindAdapterEx*函数或*ProtocolUnbindAdapterEx*函数。

如果协议驱动程序必须启动一个操作以关闭一个绑定，该驱动程序可以调用[ **NdisUnbindAdapter**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndisunbindadapter)。 **NdisUnbindAdapter**计划在 NDIS 调用结果的工作项*ProtocolUnbindAdapterEx*。 此工作项可以运行之前调用**NdisUnbindAdapter**返回。 因此，驱动程序编写人员必须假定绑定句柄无效后**NdisUnbindAdapter**返回。

如果协议驱动程序返回 NDIS\_状态\_从 PENDING *ProtocolUnbindAdapterEx*，它必须调用[ **NdisCompleteUnbindAdapterEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscompleteunbindadapterex)最终状态为完成绑定请求。

如果 NDIS 返回 NDIS\_状态\_从 PENDING **NdisCloseAdapterEx**，NDIS 更高版本调用协议驱动程序[ *ProtocolCloseAdapterCompleteEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_close_adapter_complete_ex)函数。

可以调用 NDIS *ProtocolUnbindAdapterEx*如果绑定处于已暂停状态。

取消绑定的所有操作都都完成后，该绑定将处于未绑定状态。

 

 





