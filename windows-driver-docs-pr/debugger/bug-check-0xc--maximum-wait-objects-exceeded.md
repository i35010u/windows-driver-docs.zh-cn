---
title: Bug 检查 0xC MAXIMUM_WAIT_OBJECTS_EXCEEDED
description: MAXIMUM_WAIT_OBJECTS_EXCEEDED bug 检查具有 0x0000000C 值。 这表示当前线程的已超出允许的等待对象数。
ms.assetid: 99d2eb8f-f331-45b8-a96b-68696802c269
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
ms.openlocfilehash: 93202d4febfc2dd88c4049d19985f955dab359eb
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902559"
---
# <a name="bug-check-0xc-maximumwaitobjectsexceeded"></a>Bug 检查 0xC：最大\_等待\_对象\_超出


最大值\_等待\_对象\_超出错误检查的值为 0x0000000C。 这表示当前线程的已超出允许的等待对象数。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="maximumwaitobjectsexceeded-parameters"></a>最大\_等待\_对象\_超出参数


无

<a name="cause"></a>原因
-----

此 bug 检查而得出的使用不当**KeWaitForMultipleObjects**或**FsRtlCancellableWaitForMultipleObjects**。

调用方可能会将指针传递到此例程中的缓冲区*WaitBlockArray*参数。 系统将使用此缓冲区来跟踪等待对象。

如果提供一个缓冲区，则*计数*参数不能超过最大值\_等待\_对象。 如果未不提供任何缓冲区，则*计数*参数不能超过线程\_等待\_对象。

如果的值*计数*超过了允许的值，发出此 bug 检查。

 

 




