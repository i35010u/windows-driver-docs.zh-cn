---
title: NDKPI 推迟的处理方案
description: 本部分介绍用于 NDKPI 推迟的处理
ms.assetid: DA2D0FCA-D84B-4599-A560-8F87A0918D99
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 49365eafcb7d8b27aa033d67150e02c0242d2acf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566198"
---
# <a name="ndkpi-deferred-processing-scheme"></a>NDKPI 延迟处理方案


有很多情况下，其中 NDK 使用者将发布的发起程序请求链到队列对 (QP)。 例如，使用者可以将发布发送请求后跟的快速注册请求的数。 此类请求模式的性能可能改进了如果在一系列请求排队发送至 QP，然后指定给处理作为一个批处理中，而不表示对硬件链中的每个请求，一一硬件。

**NDK\_OP\_标志\_DEFER**标志值可用于此用途，以下请求类型：

-   *NdkBind* ([*NDK\_FN\_BIND*](https://msdn.microsoft.com/library/windows/hardware/hh439859))
-   *NdkFastRegister* ([*NDK\_FN\_FAST\_REGISTER*](https://msdn.microsoft.com/library/windows/hardware/hh439887))
-   *NdkInvalidate* ([*NDK\_FN\_INVALIDATE*](https://msdn.microsoft.com/library/windows/hardware/hh439901))
-   *NdkRead* ([*NDK\_FN\_READ*](https://msdn.microsoft.com/library/windows/hardware/hh439906))
-   *NdkSend* ([*NDK\_FN\_SEND*](https://msdn.microsoft.com/library/windows/hardware/hh439914))
-   *NdkSendAndInvalidate* ([*NDK\_FN\_SEND\_AND\_INVALIDATE*](https://msdn.microsoft.com/library/windows/hardware/dn265507))
-   *NdkWrite* ([*NDK\_FN\_WRITE*](https://msdn.microsoft.com/library/windows/hardware/hh439917))

标志的状态显示是对 NDK 提供程序，它可能会延迟，该值指示对硬件进行处理，请求，但该提供程序可能在任何时候处理新请求的提示。

是否存在**NDK\_OP\_标志\_DEFER**发起程序请求上的标志不会更改 NDK 提供程序的现有职责相对于生成完成。 对返回的故障状态的发起程序请求的调用必须导致列队到失败请求的 CQ 的完成。 相反，返回成功状态的调用必须最终会生成要排队发送至的 CQ，只要使用者遵循下面列出的其他要求的完成。

除了所有现有 NDK 要求，必须遵守两个额外的要求 （一个提供程序），一个用于使用者以避免出现情况，在其中请求已成功发布到与 QP **NDK\_操作\_标志\_DEFER**标志，但永远不会指定给处理的硬件：

-   提供程序时从发起程序请求的调用返回的故障状态时，必须确保所有请求的使用之前已提交**NDK\_OP\_标志\_DEFER**标志是指示对硬件进行处理。
-   使用者可保证，如果没有内联失败，所有发起程序请求链会终止不会设置的发起程序请求**NDK\_OP\_标志\_DEFER**标志。

例如，考虑具有情况下，使用者的两个快速注册请求并发送它需要发布到 QP 链：

1.  使用者将发布使用的第一个快速寄存器**NDK\_OP\_标志\_DEFER**标志并*NdkFastRegister*返回状态\_成功。
2.  同样，与发布的第二个快速寄存器**NDK\_OP\_标志\_DEFER**但现在设置标志*NdkFastRegister*返回失败状态。 在这种情况下，使用者，将无法发布发送请求。
3.  返回到第二个调用的内联失败时*NdkFastRegister*，NDK 提供程序可确保所有以前 unindicated 的请求 （在这种情况下注册的第一个快速） 指定给处理的硬件。
4.  因为第一次调用到*NdkFastRegister*成功，完成必须生成到的 CQ。
5.  因为第二个调用到*NdkFastRegister*失败以内联方式完成必须不生成到的 CQ。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






