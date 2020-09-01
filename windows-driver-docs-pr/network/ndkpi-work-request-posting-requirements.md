---
title: NDKPI 工作请求发布要求
description: 本部分介绍 NDKPI 工作请求投递的要求
ms.assetid: 2BF6F253-FCB4-4A61-9A67-81092F3C44E4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57d237ba8cd2a36d3caa2e119ec4df47f47b08e1
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210159"
---
# <a name="ndkpi-work-request-posting-requirements"></a>NDKPI 工作请求发布要求


## <a name="work-request-posting-rules-for-the-consumer"></a>使用者的工作请求过帐规则


NDK 使用者将在发起方队列上发布以下类型的工作请求：

-   *NdkBind* ([*NDK \_ FN \_ BIND*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_bind)) 
-   *NdkFastRegister* ([*NDK \_ FN \_ FAST \_ REGISTER*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_fast_register)) 
-   *NdkInvalidate* ([*NDK \_ FN \_ 无效*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_invalidate)) 
-   *NdkRead* ([*NDK \_ FN \_ READ*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_read)) 
-   *NdkSend* ([*NDK \_ FN \_ SEND*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send)) 
-   *NdkSendAndInvalidate* ([*NDK \_ FN \_ SEND \_ 和 \_ 无效*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate)) 
-   *NdkWrite* ([*NDK \_ FN \_ 写入*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_write)) 

使用者将在接收队列上发布 *NdkReceive* ([*NDK \_ FN \_ receive*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_receive)) 请求。

使用者会以序列化方式将所有这些请求发布到 [**NDK \_ QP**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp) 或 [**ndk \_ .srq**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq) 上的同一单独队列。 换言之，使用者永远不会对属于 **NDK \_ QP** 或 **ndk \_ .srq**的同一单独队列上的任何工作请求函数进行两次并发调用。

例如，这意味着不会发出并发*NdkReceive*调用，不会发出并发*NdkSend*和*NdkWrite*调用，但是可以在同一[**NDK \_ QP**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)上发出并发*NdkReceive*和*NdkWrite*调用。

## <a name="work-request-posting-rules-for-the-provider"></a>提供程序的工作请求过帐规则


该提供程序在上述工作请求函数内不应具有任何冗余锁，因为它可以保证由使用者对其进行序列化。

提供程序必须能够处理 *NdkFlush* ([*NDK \_ FN \_ FLUSH*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_flush)) 调用，这些调用可以与同一 [**NDK \_ QP**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)上的工作请求调用同时调用。

提供程序必须能够处理[**NDK \_ **](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)) 的后续[**ndk \_ 连接器**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)对象上的**NdkCloseConnector**调用 (，该对象可与同一**ndk \_ qp**上的工作请求调用同时调用。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md)

 

