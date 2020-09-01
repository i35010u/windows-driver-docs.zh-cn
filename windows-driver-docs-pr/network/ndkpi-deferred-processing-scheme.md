---
title: NDKPI 延迟处理方案
description: 本部分介绍用于 NDKPI 的延迟处理
ms.assetid: DA2D0FCA-D84B-4599-A560-8F87A0918D99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4737bdd18413a5bcded419969696074b0eb7e3b3
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216154"
---
# <a name="ndkpi-deferred-processing-scheme"></a>NDKPI 延迟处理方案


在许多情况下，NDK 使用者会将发起方请求链发送到队列对 (QP) 。 例如，使用者可以发布大量快速注册请求，后跟发送请求。 如果请求的链排入到 QP，并向其指出要以批处理形式处理的硬件，则可以提高此类请求模式的性能，而不是逐个指示每个到硬件的请求。

对于以下请求类型， **NDK 操作 \_ \_ 标志 \_ 延迟** 标志值可以用于此目的：

-   *NdkBind* ([*NDK \_ FN \_ BIND*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_bind)) 
-   *NdkFastRegister* ([*NDK \_ FN \_ FAST \_ REGISTER*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_fast_register)) 
-   *NdkInvalidate* ([*NDK \_ FN \_ 无效*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_invalidate)) 
-   *NdkRead* ([*NDK \_ FN \_ READ*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_read)) 
-   *NdkSend* ([*NDK \_ FN \_ SEND*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send)) 
-   *NdkSendAndInvalidate* ([*NDK \_ FN \_ SEND \_ 和 \_ 无效*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate)) 
-   *NdkWrite* ([*NDK \_ FN \_ 写入*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_write)) 

该标志的存在是对 NDK 提供程序的提示，它可能会延迟指出要处理的硬件请求，但提供程序可以随时处理新请求。

发起方请求上出现 **ndk 操作 \_ \_ 标志 \_ 延迟** 标志后，不会更改 NDK 提供程序在生成完成方面的现有责任。 对返回失败状态的发起方请求的调用不得导致完成排队等待失败请求的 CQ。 相反，只要使用者遵循下面所列的其他要求，返回成功状态的调用就必须最终导致完成排队到 CQ。

除了所有的现有 NDK 要求外，另外两个要求 (一个提供给提供程序，另一个用于使用者) ，以防止使用 **NDK 操作 \_ \_ 标志 \_ 延迟** 标志将请求成功地发送到 QP，但从不指示用于处理的硬件的其他要求：

-   当从对发起方请求的调用返回失败状态时，提供程序必须保证以前使用 **NDK 操作 \_ \_ 标志 \_ 延迟** 标志提交的所有请求都将指示用于处理硬件。
-   使用者可以保证，在未发生内联故障的情况下，所有发起程序请求链都将被未设置 **NDK 操作 \_ \_ 标志 \_ 延迟** 标志的发起程序请求终止。

例如，假设使用者具有两个快速注册请求的链和需要发布到 QP 的发送：

1.  使用者将第一个快速注册与 **NDK 操作 \_ \_ 标志 \_ 延迟** 标志一起发布， *NdkFastRegister* 返回状态 \_ SUCCESS。
2.  同样，第二个快速注册将与 **NDK \_ OP \_ 标志 \_ 延迟** 标志集一起发布，但现在 *NdkFastRegister* 返回失败状态。 在这种情况下，使用者将不会发布发送请求。
3.  当第二次调用 *NdkFastRegister*时返回内联失败时，在这种情况下，NDK 提供程序将确保所有之前 unindicated 的请求都 (第一个 fast 注册，) 被指示到硬件进行处理。
4.  由于对 *NdkFastRegister* 的第一次调用成功，因此必须在 CQ 中生成完成。
5.  由于对 *NdkFastRegister* 的第二次调用失败，因此不能在 CQ 中生成完成。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md)

 

