---
title: NDKPI 工作请求发布要求
description: 本部分介绍 NDKPI 工作请求发布要求
ms.assetid: 2BF6F253-FCB4-4A61-9A67-81092F3C44E4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4182ffa518121beab9ac7ac71d12629f29731654
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67364021"
---
# <a name="ndkpi-work-request-posting-requirements"></a>NDKPI 工作请求发布要求


## <a name="work-request-posting-rules-for-the-consumer"></a>对于使用者发布规则的工作请求


NDK 使用者会发起方队列中发布以下类型的工作请求：

-   *NdkBind* ([*NDK\_FN\_BIND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_bind))
-   *NdkFastRegister* ([*NDK\_FN\_FAST\_REGISTER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_fast_register))
-   *NdkInvalidate* ([*NDK\_FN\_INVALIDATE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_invalidate))
-   *NdkRead* ([*NDK\_FN\_READ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_read))
-   *NdkSend* ([*NDK\_FN\_SEND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_send))
-   *NdkSendAndInvalidate* ([*NDK\_FN\_SEND\_AND\_INVALIDATE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate))
-   *NdkWrite* ([*NDK\_FN\_WRITE*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_write))

使用者将发布*使 NdkReceive* ([*NDK\_FN\_接收*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_receive)) 上接收队列的请求。

使用者将发布所有这些请求到相同的单个队列上[ **NDK\_QP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp)或[ **NDK\_SRQ** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_srq)以序列化的方式。 换而言之，使用者再也不会对请求的任何工作函数的两个并发调用上属于同一个单个队列**NDK\_QP**或**NDK\_SRQ**。

这意味着，例如，该并发*使 NdkReceive*的调用不会颁发、 并发*NdkSend*并*NdkWrite*不会发出调用，但并发*使 NdkReceive*并*NdkWrite*调用可能会对相同发出[ **NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp)。

## <a name="work-request-posting-rules-for-the-provider"></a>为提供程序发布规则的工作请求


提供程序不应具有更高版本的工作请求函数内部的任何冗余锁，因为可确保由使用者要序列化。

提供程序必须能够处理*NdkFlush* ([*NDK\_FN\_刷新*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/nc-ndkpi-ndk_fn_flush)) 可能与工作并发调用的调用上请求调用相同[ **NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp)。

提供程序必须能够处理**NdkCloseConnector**调用 (在后续任务[ **NDK\_连接器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_connector)对象[ **NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_qp))，不能与工作请求调用同时对调用相同**NDK\_QP**。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






