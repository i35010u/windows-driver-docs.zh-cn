---
title: NDKPI 对象生存期要求
description: 本部分介绍 NDKPI 对象生存期要求
ms.assetid: 94993523-D0D7-441E-B95C-417800840BAC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8b59e31e8c09007a36a9a8004e3bcd07612efe4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542191"
---
# <a name="ndkpi-object-lifetime-requirements"></a>NDKPI 对象生存期要求


## <a name="how-ndk-objects-are-created-used-and-closed"></a>如何创建、 使用和关闭 NDK 对象


NDK 使用者通过该对象调用 NDK 提供程序的创建函数启动的 NDK 对象创建请求。

当使用者调用创建函数时，会传递*NdkCreateCompletion* ([*NDK\_FN\_创建\_完成*](https://msdn.microsoft.com/library/windows/hardware/hh439871)) 作为参数。

使用者通过调用中传递的对象的调度表的提供程序函数来启动各种请求*NdkRequestCompletion* ([*NDK\_FN\_请求\_完成*](https://msdn.microsoft.com/library/windows/hardware/hh439912)) 作为参数的完成回调。

当不再需要对象时，使用者调用提供程序的*NdkCloseObject* ([*NDK\_FN\_关闭\_对象*](https://msdn.microsoft.com/library/windows/hardware/hh439863)) 函数以初始化该对象的关闭请求传递*NdkCloseCompletion* ([*NDK\_FN\_关闭\_完成*](https://msdn.microsoft.com/library/windows/hardware/hh439862)) 作为参数的回调。

对于所有此类函数，该提供程序调用使用者的回调函数来完成该请求。 此调用指示向使用者，该提供程序已完成操作 （例如，关闭对象），并且正在将控制返回给使用者。

## <a name="the-rules-for-completion-callbacks"></a>有关完成回调的规则


提供程序时提供程序已在使用者的请求时创建了对象，调用使用者的*NdkCreateCompletion*指示对象是否准备好用于回调。

而无需等待要返回的第一个回调，使用者可以为同一对象调用其他提供程序函数。

使用者将不会调用*NdkCloseObject*直到该对象的所有提供程序函数已返回的对象的函数。

但是，如果提供程序函数会初始化完成请求，使用者可以随意调用*NdkCloseObject*从内完成该回叫，即使如果未返回提供程序函数。

通过执行以下任一操作从回调返回之前，提供程序函数可以开始完成请求：

-   直接调用完成回调
-   队列到另一个线程完成请求

通过将完成请求，该提供程序有效地控制返回给使用者。 提供程序必须假定，可以在任何时间提供程序启动完成请求后关闭该对象。

**请注意**  以防止死锁在启动完成请求后，该提供程序必须是：

-   完成回调返回之前，不执行对象上的其他操作。
-   如果提供程序必须绝对接触到对象，请采取必要的措施来保持不变，该对象。

 

## <a name="example-consumer-provider-interaction"></a>示例：使用者提供程序交互


请考虑以下方案：

1.  使用者创建一个连接器 ([**NDK\_连接器**](https://msdn.microsoft.com/library/windows/hardware/hh439852))，然后调用*NdkConnect* ([*NDK\_FN\_CONNECT*](https://msdn.microsoft.com/library/windows/hardware/hh439865))。
2.  提供程序处理连接请求、 遇到故障时，并调用的上下文中的使用者的完成回调*NdkConnect*调用 （而不是返回内联失败由于一个内部实现的选择）。
3.  使用者可调用*NdkCloseObject*上下文中的此完成回调，即使*NdkConnect*调用尚未返回给使用者。

若要避免死锁，该提供程序必须不接触连接器对象在步骤 2 后 (点时它启动，在完成回调*NdkConnect*调用)。

## <a name="closing-antecedent-and-successor-objects"></a>关闭前面的任务和后续任务对象


提供程序必须做好使用者调用*NdkCloseObject*函数来关闭之前的使用者调用的前面对象*NdkCloseObject*的后续任务对象。 如果使用者这样做，下面是该提供程序必须执行的操作：

-   提供程序必须关闭 antecedent 对象，直到关闭所有后续任务对象，即，提供程序必须返回状态\_PENDING 从关闭请求，并完成它 (通过调用已注册*NdkCloseCompletion*函数关闭请求) 一旦所有后续对象被都关闭。
-   使用者不得将 antecedent 对象之后调用*NdkCloseObject*它，因此该提供程序不需要添加任何处理由于前面的对象的更多提供程序函数 （但它可能当它选择）。
-   提供程序可能会视作关闭请求一个简单的取消引用具有没有其他负面影响之前的最后一个的后继对象已关闭，除非另有要求 （低于该值的 NDK 侦听器关闭情况具有所需的负面影响，请参阅）。

提供程序必须完成前面对象上的关闭请求 (包括[ **NDK\_适配器**](https://msdn.microsoft.com/library/windows/hardware/hh439848)关闭请求) 在任何后继任何正在进行中关闭完成回调之前对象返回到提供程序。 这是为了允许安全地卸载 NDK 使用者。

NDK 使用者将不会调用*NdkCloseObject*有关[ **NDK\_适配器**](https://msdn.microsoft.com/library/windows/hardware/hh439848)对象 （这是阻止调用） 从使用者的回调函数内。

## <a name="closing-adapter-objects"></a>关闭适配器对象


请考虑以下方案：

1.  使用者可调用*NdkCloseObject*上完成队列 (CQ) 对象。
2.  访问接口将返回状态\_挂起，及更高版本调用使用者的完成回调。
3.  在完成此回调中，使用者发出信号事件，它现在是确定以关闭 NDK\_适配器。
4.  另一个线程唤醒时此信号，并关闭[ **NDK\_适配器**](https://msdn.microsoft.com/library/windows/hardware/hh439848)并继续执行卸载。
5.  但是，在调用使用者的 CQ 关闭完成回调的线程可能仍在使用者的回调函数 (例如，函数[epilog](https://msdn.microsoft.com/library/tawsa7cb.aspx))，因此是不安全的要卸载的使用者驱动程序。
6.  因为完成回调上下文是唯一的上下文使用者可以发出事件信号，使用者驱动程序不能解决安全卸载问题本身。

必须在其使用者可以确保所有其回调返回控件的点。 NDKPI，在此点是何时关闭请求上的[ **NDK\_适配器**](https://msdn.microsoft.com/library/windows/hardware/hh439848)返回控件。 请注意， **NDK\_适配器**关闭请求是阻止调用。 当**NDK\_适配器**关闭请求返回，它可保证，所有对象上的所有回调，都根据该**NDK\_适配器**对象返回到控件提供程序。

## <a name="completing-close-requests"></a>完成关闭请求


提供程序必须完成的对象，直到上一个关闭请求：

-   所有挂起的异步请求的对象上都完成后 （换句话说，它们的完成回调已返回到提供程序时）。
-   所有使用者的事件的回调 (例如， *NdkCqNotificationCallback* ([*NDK\_FN\_CQ\_通知\_回调*](https://msdn.microsoft.com/library/windows/hardware/hh439870)) 上的 CQ *NdkConnectEventCallback* ([*NDK\_FN\_CONNECT\_事件\_回调* ](https://msdn.microsoft.com/library/windows/hardware/hh439867)) 对侦听器) 返回了错误的提供程序。

提供程序必须确保不再使用回调会调用关闭完成回调后或在关闭请求返回状态\_成功。 请注意，任何所需刷新或取消的挂起的异步请求还必须启动关闭请求。

**请注意**  它以逻辑方式遵循从上述 NDK 使用者必须不调用*NdkCloseObject*有关[ **NDK\_适配器**](https://msdn.microsoft.com/library/windows/hardware/hh439848)对象 （这是阻止调用） 从使用者的回调函数内。

 

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






