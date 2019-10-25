---
title: NDKPI 工作请求发布要求
description: 本部分介绍 NDKPI 工作请求投递的要求
ms.assetid: 2BF6F253-FCB4-4A61-9A67-81092F3C44E4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7df322909559045a3412a3b471558c0e5cf80ead
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829107"
---
# <a name="ndkpi-work-request-posting-requirements"></a>NDKPI 工作请求发布要求


## <a name="work-request-posting-rules-for-the-consumer"></a>使用者的工作请求过帐规则


NDK 使用者将在发起方队列上发布以下类型的工作请求：

-   *NdkBind* （[*NDK\_FN\_BIND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_bind)）
-   *NdkFastRegister* （[*NDK\_FN\_快速\_寄存器*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_fast_register)）
-   *NdkInvalidate* （[*NDK\_FN\_无效*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_invalidate)）
-   *NdkRead* （[*NDK\_FN\_READ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_read)）
-   *NdkSend* （[*NDK\_FN\_发送*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send)）
-   *NdkSendAndInvalidate* （[*NDK\_FN\_发送\_，\_无效*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate)）
-   *NdkWrite* （[*NDK\_FN\_写入*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_write)）

使用者将在接收队列上发布*NdkReceive* （[*NDK\_FN\_接收*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_receive)）请求。

使用者会以序列化方式将所有这些请求发布到[**NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)或[**ndk\_.srq**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_srq)上的同一单独队列。 换言之，使用者永远不会对属于**NDK\_QP**或**ndk\_.srq**的同一单独队列上的任何工作请求函数进行两次并发调用。

例如，这意味着不会发出并发*NdkReceive*调用，不会发出并发*NdkSend*和*NdkWrite*调用，但是可以在同一 NDK 上发出并发*NdkReceive*和*NdkWrite*调用[ **\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)。

## <a name="work-request-posting-rules-for-the-provider"></a>提供程序的工作请求过帐规则


该提供程序在上述工作请求函数内不应具有任何冗余锁，因为它可以保证由使用者对其进行序列化。

提供程序必须能够处理*NdkFlush* （[*NDK\_FN\_FLUSH*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_flush)）调用，这些调用可以与同一[**NDK\_QP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)上的工作请求调用同时调用。

提供程序必须能够处理对[**ndk\_qp**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_qp)的后续[**NDK\_连接器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)对象的**NdkCloseConnector**调用，该调用可能会与同一**NDK\_QP**上的工作请求调用同时调用。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口（NDKPI）](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






