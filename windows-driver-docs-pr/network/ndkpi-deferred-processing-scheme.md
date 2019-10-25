---
title: NDKPI 延迟处理方案
description: 本部分介绍用于 NDKPI 的延迟处理
ms.assetid: DA2D0FCA-D84B-4599-A560-8F87A0918D99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 117a5a871fd87a5eb686a11c487fc5e80f8d01c1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831901"
---
# <a name="ndkpi-deferred-processing-scheme"></a>NDKPI 延迟处理方案


在许多情况下，NDK 使用者会将发起方请求链发布到队列对（QP）。 例如，使用者可以发布大量快速注册请求，后跟发送请求。 如果请求的链排入到 QP，并向其指出要以批处理形式处理的硬件，则可以提高此类请求模式的性能，而不是逐个指示每个到硬件的请求。

使用以下请求类型可将**NDK\_OP\_标志\_延迟**标志值用于此目的：

-   *NdkBind* （[*NDK\_FN\_BIND*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_bind)）
-   *NdkFastRegister* （[*NDK\_FN\_快速\_寄存器*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_fast_register)）
-   *NdkInvalidate* （[*NDK\_FN\_无效*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_invalidate)）
-   *NdkRead* （[*NDK\_FN\_READ*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_read)）
-   *NdkSend* （[*NDK\_FN\_发送*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send)）
-   *NdkSendAndInvalidate* （[*NDK\_FN\_发送\_，\_无效*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_send_and_invalidate)）
-   *NdkWrite* （[*NDK\_FN\_写入*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_write)）

该标志的存在是对 NDK 提供程序的提示，它可能会延迟指出要处理的硬件请求，但提供程序可以随时处理新请求。

在发起方请求上出现**ndk\_OP\_标志\_延迟**标志并不会更改 NDK 提供程序与生成完成相关的现有责任。 对返回失败状态的发起方请求的调用不得导致完成排队等待失败请求的 CQ。 相反，只要使用者遵循下面所列的其他要求，返回成功状态的调用就必须最终导致完成排队到 CQ。

除了所有的现有 NDK 要求外，还必须观察到另外两个要求（一个用于提供程序，一个用于使用者），以防止请求成功通过**NDK\_OP\_标志发送到 QP\_延迟**标志，但从不指示用于处理的硬件：

-   当从对发起方请求的调用返回失败状态时，提供程序必须保证先前使用**NDK\_OP\_\_标志**提交的所有请求都向硬件指示，以便进行处理。
-   使用者可以保证，在未发生内联故障的情况下，所有发起程序请求链都将被未设置**NDK\_OP\_标志\_延迟**标志的发起程序请求终止。

例如，假设使用者具有两个快速注册请求的链和需要发布到 QP 的发送：

1.  使用者将第一个快速注册与**NDK\_OP\_标志一起发布\_延迟**标志， *NdkFastRegister*返回状态\_成功。
2.  同样，第二个快速注册与**NDK\_OP\_标志一起发布\_延迟**标志集，但现在*NdkFastRegister*返回失败状态。 在这种情况下，使用者将不会发布发送请求。
3.  当第二次调用*NdkFastRegister*时返回内联失败时，NDK 提供程序会确保所有之前 unindicated 的请求（在本例中为第一个快速寄存器）都指示用于处理的硬件。
4.  由于对*NdkFastRegister*的第一次调用成功，因此必须在 CQ 中生成完成。
5.  由于对*NdkFastRegister*的第二次调用失败，因此不能在 CQ 中生成完成。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口（NDKPI）](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






