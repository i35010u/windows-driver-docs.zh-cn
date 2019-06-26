---
title: 实现 NDKPI 函数
description: NDK 支持的微型端口驱动程序必须注册所有 NDK_FN_XXX 的回调函数的入口点。 所有 NDKPI 提供程序回调函数都是必需的;无是可选的。
ms.assetid: 9A7D5F77-C26A-47B6-9F8E-ECB80D4FF384
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0b8a4b52c54dcd2e211190d9f454eb307687e91
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67374856"
---
# <a name="implementing-ndkpi-functions"></a>实现 NDKPI 函数


NDK 支持的微型端口驱动程序必须注册所有的入口点[NDK\_FN\_*XXX*回调函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)。 所有 NDKPI 提供程序回调函数都是必需的;无是可选的。

若要注册这些函数的支持，微型端口驱动程序存储其入口点在"对象的调度表"中列出的结构中的以下表的列：

| 对象类型                                               | 此函数所创建的                                                                                                       | 对象的调度表                                                      |
|-----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| [**NDK\_ADAPTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_adapter)                  | [*OPEN\_NDK\_ADAPTER\_HANDLER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndisndk/nc-ndisndk-open_ndk_adapter_handler)                                                             | [**NDK\_适配器\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_adapter_dispatch)                  |
| [**NDK\_连接器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector)              | [*NDK\_FN\_CREATE\_CONNECTOR*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_connector)                                                               | [**NDK\_连接器\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector_dispatch)              |
| [**NDK\_CQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_cq)                            | [*NDK\_FN\_CREATE\_CQ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_cq)                                                                             | [**NDK\_CQ\_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_cq_dispatch)                            |
| [**NDK\_LISTENER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_listener)                | [*NDK\_FN\_CREATE\_LISTENER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_listener)                                                                 | [**NDK\_侦听器\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_listener_dispatch)                |
| [**NDK\_MR**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mr)                            | [*NDK\_FN\_CREATE\_MR*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_mr)                                                                             | [**NDK\_MR\_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mr_dispatch)                            |
| [**NDK\_MW**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mw)                            | [*NDK\_FN\_CREATE\_MW*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_mw)                                                                             | [**NDK\_MW\_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_mw_dispatch)                            |
| [**NDK\_PD**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_pd)                            | [*NDK\_FN\_CREATE\_PD*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_pd)                                                                             | [**NDK\_PD\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_pd_dispatch)                            |
| [**NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp)                            | [*NDK\_FN\_创建\_QP* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_qp)或[ *NDK\_FN\_创建\_QP\_WITH\_SRQ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_qp_with_srq)   | [**NDK\_QP\_调度**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp_dispatch)                            |
| [**NDK\_SHARED\_ENDPOINT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_shared_endpoint) | [*NDK\_FN\_CREATE\_SHARED\_ENDPOINT*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_shared_endpoint)                                                  | [**NDK\_SHARED\_ENDPOINT\_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_shared_endpoint_dispatch) |
| [**NDK\_SRQ**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_srq)                          | [*NDK\_FN\_创建\_SRQ* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_srq)或[ *NDK\_FN\_创建\_QP\_WITH\_SRQ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_create_qp_with_srq) | [**NDK\_SRQ\_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_srq_dispatch)                          |

 

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






