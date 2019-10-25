---
title: 实现 NDKPI 函数
description: 支持 NDK 的微型端口驱动程序必须为所有 NDK_FN_XXX 回调函数注册入口点。 所有 NDKPI 提供程序回调函数都是必需的;none 是可选的。
ms.assetid: 9A7D5F77-C26A-47B6-9F8E-ECB80D4FF384
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01b92c918f5df6f5ec435d0e1f42ea057851cd39
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72833856"
---
# <a name="implementing-ndkpi-functions"></a>实现 NDKPI 函数


支持 NDK 的微型端口驱动程序必须为所有[ndk\_FN\_*XXX*回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)注册入口点。 所有 NDKPI 提供程序回调函数都是必需的;none 是可选的。

为注册对这些函数的支持，微型端口驱动程序将其入口点存储在下表的 "对象的调度表" 列中列出的结构中：

| 对象类型                                               | 此函数创建的                                                                                                       | 对象的调度表                                                      |
|-----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| [**NDK\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)                  | [*打开\_NDK\_适配器\_处理程序*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndisndk/nc-ndisndk-open_ndk_adapter_handler)                                                             | [**NDK\_适配器\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter_dispatch)                  |
| [**NDK\_连接器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)              | [*NDK\_FN\_创建\_连接器*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_connector)                                                               | [**NDK\_连接器\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector_dispatch)              |
| [**NDK\_CQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq)                            | [*NDK\_FN\_创建\_CQ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_cq)                                                                             | [**NDK\_CQ\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq_dispatch)                            |
| [**NDK\_侦听器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener)                | [*NDK\_FN\_创建\_侦听器*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_listener)                                                                 | [**NDK\_侦听器\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener_dispatch)                |
| [**NDK\_MR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mr)                            | [*NDK\_FN\_创建\_MR*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_mr)                                                                             | [**NDK\_尊敬的\_派单**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mr_dispatch)                            |
| [**NDK\_MW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mw)                            | [*NDK\_FN\_CREATE\_MW*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_mw)                                                                             | [**NDK\_MW\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mw_dispatch)                            |
| [**NDK\_PD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_pd)                            | [*NDK\_FN\_创建\_PD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_pd)                                                                             | [**NDK\_PD\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_pd_dispatch)                            |
| [**NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)                            | [*NDK\_fn\_创建\_QP*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_qp)或[ *NDK\_FN\_通过\_.srq 创建\_QP\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_qp_with_srq)   | [**NDK\_QP\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp_dispatch)                            |
| [**NDK\_共享\_终结点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint) | [*NDK\_FN\_创建\_共享\_终结点*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_shared_endpoint)                                                  | [**NDK\_共享\_终结点\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint_dispatch) |
| [**NDK\_.SRQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq)                          | [*NDK\_fn\_创建\_.srq*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_srq)或[ *NDK\_FN\_通过\_.srq 创建\_QP\_* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_qp_with_srq) | [**NDK\_.SRQ\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq_dispatch)                          |

 

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口（NDKPI）](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






