---
title: 实现 NDKPI 函数
description: 支持 NDK 的微型端口驱动程序必须注册所有 NDK_FN_XXX 回调函数的入口点。 所有 NDKPI 提供程序回调函数都是必需的;none 是可选的。
ms.assetid: 9A7D5F77-C26A-47B6-9F8E-ECB80D4FF384
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7d8a307c055ec7daed36164e5488bc119010f2d9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217610"
---
# <a name="implementing-ndkpi-functions"></a>实现 NDKPI 函数


支持 NDK 的微型端口驱动程序必须为所有[ndk \_ FN \_ *XXX*回调函数](/windows-hardware/drivers/ddi/_netvista/)注册入口点。 所有 NDKPI 提供程序回调函数都是必需的;none 是可选的。

为注册对这些函数的支持，微型端口驱动程序将其入口点存储在下表的 "对象的调度表" 列中列出的结构中：

| 对象类型                                               | 此函数创建的                                                                                                       | 对象的调度表                                                      |
|-----------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------|
| [**NDK \_ 适配器**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)                  | [*打开 \_ NDK \_ 适配器 \_ 处理程序*](/windows-hardware/drivers/ddi/ndisndk/nc-ndisndk-open_ndk_adapter_handler)                                                             | [**NDK \_ 适配器 \_ 调度**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter_dispatch)                  |
| [**NDK \_ 连接器**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)              | [*NDK \_ FN \_ 创建 \_ 连接器*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_connector)                                                               | [**NDK \_ 连接器 \_ 调度**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector_dispatch)              |
| [**NDK \_ CQ**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq)                            | [*NDK \_ FN \_ CREATE \_ CQ*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_cq)                                                                             | [**NDK \_ CQ \_ 调度**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_cq_dispatch)                            |
| [**NDK \_ 侦听器**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener)                | [*NDK \_ FN \_ CREATE \_ 侦听器*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_listener)                                                                 | [**NDK \_ 侦听器 \_ 调度**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_listener_dispatch)                |
| [**NDK \_ MR**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mr)                            | [*NDK \_ FN \_ CREATE \_ MR*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_mr)                                                                             | [**NDK \_ MR \_ 派单**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mr_dispatch)                            |
| [**NDK \_ MW**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mw)                            | [*NDK \_ FN \_ CREATE \_ MW*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_mw)                                                                             | [**NDK \_ MW \_ 派单**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_mw_dispatch)                            |
| [**NDK \_ PD**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_pd)                            | [*NDK \_ FN \_ CREATE \_ PD*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_pd)                                                                             | [**NDK \_ PD \_ 调度**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_pd_dispatch)                            |
| [**NDK \_ QP**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)                            | [*NDK \_FN \_ create \_ Qp*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_qp)或[ *NDK \_ FN \_ create \_ qp \_ WITH \_ .srq*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_qp_with_srq)   | [**NDK \_ QP \_ 调度**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp_dispatch)                            |
| [**NDK \_ 共享 \_ 终结点**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint) | [*NDK \_ FN \_ CREATE \_ SHARED \_ ENDPOINT*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_shared_endpoint)                                                  | [**NDK \_ 共享 \_ 终结点 \_ 调度**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_shared_endpoint_dispatch) |
| [**NDK \_ .SRQ**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq)                          | [*NDK \_FN \_ create \_ .Srq*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_srq)或[ *NDK \_ FN \_ create \_ QP \_ WITH \_ .srq*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_qp_with_srq) | [**NDK \_ .SRQ \_ 调度**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq_dispatch)                          |

 

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md)

 

