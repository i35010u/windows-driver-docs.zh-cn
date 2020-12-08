---
title: Bug 检查 0xC MAXIMUM_WAIT_OBJECTS_EXCEEDED
description: MAXIMUM_WAIT_OBJECTS_EXCEEDED bug 检查的值为0x0000000C。 这表示当前线程超出了允许的等待对象数。
keywords:
- Bug 检查 0xC MAXIMUM_WAIT_OBJECTS_EXCEEDED
- MAXIMUM_WAIT_OBJECTS_EXCEEDED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MAXIMUM_WAIT_OBJECTS_EXCEEDED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9b55bb6f342afda70167bda51756b6be84ea260e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783531"
---
# <a name="bug-check-0xc-maximum_wait_objects_exceeded"></a>Bug 检查0xC：超过最大 \_ 等待 \_ 对象数 \_


\_超过 bug 检查的最大等待 \_ 对象的值为 \_ 0x0000000C。 这表示当前线程超出了允许的等待对象数。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="maximum_wait_objects_exceeded-parameters"></a>最大 \_ 等待 \_ 对象 \_ 超出参数


无

<a name="cause"></a>原因
-----

此 bug 检查不正确使用 **KeWaitForMultipleObjects** 或 **FsRtlCancellableWaitForMultipleObjects** 的结果。

调用方可能会在此例程的 *WaitBlockArray* 参数中传递一个指向缓冲区的指针。 系统将使用此缓冲区跟踪等待对象。

如果提供了缓冲区，则 *Count* 参数可能不会超过最大 \_ 等待 \_ 对象。 如果未提供缓冲区，则 *Count* 参数可能不会超过线程 \_ 等待 \_ 对象。

如果 *Count* 的值超出了允许的值，则会发出此 bug 检查。

 

 




