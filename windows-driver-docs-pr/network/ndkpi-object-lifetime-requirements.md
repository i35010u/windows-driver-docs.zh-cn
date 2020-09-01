---
title: NDKPI 对象生存期要求
description: 本部分介绍 NDKPI 对象生存期的要求
ms.assetid: 94993523-D0D7-441E-B95C-417800840BAC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8ea8774dfcdebe6f0b3fb1562f5738ddb7ff13b
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216608"
---
# <a name="ndkpi-object-lifetime-requirements"></a>NDKPI 对象生存期要求


## <a name="how-ndk-objects-are-created-used-and-closed"></a>如何创建、使用和关闭 NDK 对象


NDK 使用者通过调用 ndk 提供程序对该对象的 create 函数来启动对该对象的创建请求。

当使用者调用 create 函数时，它会将 *NdkCreateCompletion* 作为参数传递 ([*NDK \_ FN \_ create \_ 完成*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_create_completion)) 。

使用者通过在对象的调度表中调用 provider 函数来发起各种请求，传递 *NdkRequestCompletion* ([*NDK \_ FN \_ REQUEST \_ 完成*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_request_completion)) 完成回调作为参数。

当不再需要某个对象时，使用者将调用提供程序的 *NdkCloseObject* ([*NDK \_ fn \_ close \_ 对象*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_close_object)) 函数来启动对该对象的关闭请求，同时将 *NdkCloseCompletion* ([*NDK \_ FN \_ close \_ 完成*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_close_completion)) 回调作为参数传递。

对于所有此类函数，提供程序将调用使用者的回调函数来完成请求。 此调用向使用者指示提供程序已完成操作 (例如，关闭对象) 并向使用者返回控制权。

## <a name="the-rules-for-completion-callbacks"></a>完成回调的规则


当提供程序在使用者请求时创建了对象时，提供程序将调用使用者的 *NdkCreateCompletion* 回调以指示该对象已准备就绪，可供使用。

使用者可以调用同一个对象的其他提供程序函数，而无需等待第一个回调返回。

在该对象的所有提供程序函数返回后，使用者将不会为该对象调用 *NdkCloseObject* 函数。

但是，如果提供程序函数启动完成请求，则使用者可以自由地从该完成回调内调用 *NdkCloseObject* ，即使未返回提供程序函数也是如此。

通过执行以下操作之一，提供程序函数可以在从回调返回之前启动完成请求：

-   直接调用完成回调
-   向另一个线程排队完成请求

通过启动完成请求，提供程序会有效地将控制权返回给使用者。 提供程序必须假定在提供程序启动完成请求后，可以随时关闭对象。

**注意**   若要在启动完成请求后防止死锁，提供程序必须：

-   直到完成回调返回后，才对对象执行其他操作。
-   如果提供程序绝对必须接触对象，请采取必要的措施来保持对象不变。

 

## <a name="example-consumer-provider-interaction"></a>示例：使用者提供者交互


请参考以下方案：

1.  使用者创建一个连接器 ([**NDK \_ 连接器**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_connector)) ，然后调用 *NdkConnect* ([*ndk \_ FN \_ 连接*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect)) 。
2.  该提供程序将处理连接请求，导致失败，并在 *NdkConnect* (调用的上下文中调用使用者的完成回调，而不是由于内部实现选择) 而返回内联失败。
3.  使用者在此完成回调的上下文中调用 *NdkCloseObject* ，即使 *NdkConnect* 调用尚未返回给使用者。

若要避免死锁，提供程序在第2步后不能触摸连接器对象 (在 *NdkConnect* 调用中启动完成回调时的点) 。

## <a name="closing-antecedent-and-successor-objects"></a>关闭前面的任务和后续对象


提供程序必须准备好，以便使用者可以调用 *NdkCloseObject* 函数来关闭前面的对象，然后使用者为后续对象调用 *NdkCloseObject* 。 如果使用者执行此操作，则提供程序必须执行以下操作：

-   在关闭所有后续对象之前，提供程序不能关闭前面的对象，即，提供程序必须 \_ 从关闭请求返回 "挂起" 状态，并 (通过调用已注册的 *NdkCloseCompletion* 函数关闭请求) 在所有后续对象都关闭之后。
-   使用者在对其调用 *NdkCloseObject* 后将不使用 antecedent 对象，因此，提供程序不需要添加对 antecedent (对象上的失败进一步提供程序函数的任何处理，但它可能会选择) 。
-   提供程序可以将关闭请求当作简单的取消引用（在最后一个后续任务对象关闭之前没有任何副作用），除非需要，否则 (请参阅下面具有所需副作用) 的 NDK 侦听器关闭事例。

提供程序不能在前面的对象上完成关闭请求 (包括 [**NDK \_ 适配器**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter) 关闭请求) 之前任何后续对象上的任何正在进行的关闭完成回调都返回给提供程序。 这是为了允许 NDK 使用者安全卸载。

NDK 使用者不会为[**ndk \_ 适配器**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)对象调用*NdkCloseObject* ， (是从使用者回调函数内部) 阻止调用。

## <a name="closing-adapter-objects"></a>关闭适配器对象


请参考以下方案：

1.  使用者在完成队列 (CQ) 对象上调用 *NdkCloseObject* 。
2.  提供程序返回状态 " \_ 挂起"，以后调用使用者的完成回调。
3.  在此完成回调内，使用者发出信号，指示该事件现在可以关闭 NDK \_ 适配器。
4.  另一个线程在此信号上唤醒，并关闭 [**NDK \_ 适配器**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter) 并继续卸载。
5.  但是，在其中调用使用者的 CQ close 完成回调的线程可能仍在使用者的回调函数内 (例如，函数 [epilog](/cpp/build/prolog-and-epilog)) ，因此使用者驱动程序卸载是不安全的。
6.  由于完成回调上下文是使用者可以向事件发出信号的唯一上下文，因此使用者驱动程序无法解决安全卸载问题本身。

必须有一个点，以便使用者可以确保其所有回调都已返回控制权。 在 NDKPI 中，当 [**NDK \_ 适配器**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter) 上的关闭请求返回控件时，就是这样。 请注意， **NDK \_ 适配器** 关闭请求是一种阻止调用。 当 **NDK \_ 适配器** 关闭请求返回时，保证从该 **ndk \_ 适配器** 对象的所有对象上的所有回调都已将控制权返回给提供程序。

## <a name="completing-close-requests"></a>完成关闭请求


访问接口不能完成对对象的关闭请求，直到：

-   已完成对象上所有挂起的异步请求 (换言之，它们的完成回调已经返回给提供程序) 。
-   所有使用者的事件回调 (例如* (，CQ*上的 CQ 上的*NdkConnectEventCallback* (ndk fn [* \_ \_ \_ 通知 \_ 回调*](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_cq_notification_callback)) ，) 返回到提供程序。 [* \_ \_ \_ \_ *](/windows-hardware/drivers/ddi/ndkpi/nc-ndkpi-ndk_fn_connect_event_callback)

提供程序必须保证在调用关闭完成回调之后或在关闭请求返回状态成功后，不会再进行回调 \_ 。 请注意，关闭请求还必须启动挂起的异步请求所需的任何刷新或取消操作。

**注意**   从逻辑上讲，NDK 使用者不能为[**ndk \_ 适配器**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)对象调用*NdkCloseObject* ， (是从使用者回调函数内部) 阻止调用。

 

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md)

 

