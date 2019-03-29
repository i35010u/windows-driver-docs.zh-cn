---
title: 当代码和数据应可分页
description: 当代码和数据应可分页
ms.assetid: 2804f558-8c8c-43f4-b14e-8deaac9da286
keywords:
- 内存管理 WDK 内核，可分页的驱动程序
- 可分页的驱动程序 WDK 内核，当应为可分页
- 按需锁定代码 WDK 内核
- 数值调节钮锁 WDK 内存
- 常驻代码 WDK 可分页驱动程序
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39e91814a53983a408d72500fc1cc2311deeb2de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564866"
---
# <a name="when-should-code-and-data-be-pageable"></a>代码和数据何时应可分页？





您可以使您的驱动程序的全部或部分可分页。 分页驱动程序代码可以减少驱动程序的加载图像，从而使系统空间以备他用的大小。 它是最实用的偶尔使用的设备，如调制解调器和 Cd-rom，驱动程序或驱动程序很少调用的部分。

执行以下任一的驱动程序代码必须驻留在内存中的。 也就是说，此代码必须在非分页部分中，或在代码运行时在内存中锁定的分页部分中。

-   运行在或更高版本的 IRQL = 调度\_级别。

-   获取自旋锁。

-   调用内核的对象的任何支持例程，如[ **KeReleaseMutex** ](https://msdn.microsoft.com/library/windows/hardware/ff553140)或[ **KeReleaseSemaphore**](https://msdn.microsoft.com/library/windows/hardware/ff553143)，在其中*等待*参数设置为**TRUE**。 如果使用调用内核*等待*设置为**TRUE**，则调用将返回与在调度的 IRQL\_级别。

驱动程序代码必须运行在 IRQL&lt;调度\_级别时，代码执行的任何内容，可能会导致页错误。 如果是这样的以下任何，代码可能会导致页错误：

-   访问页面缓冲池的未锁定在内存中。

-   调用的可分页的例程。

-   在用户线程的上下文中访问解锁的用户缓冲区。

通常情况下，应进行分页，如果所有可分页的代码 （或数据） 的总金额至少为 4 千字节 (KB) 的部分。 只要有可能，你应从代码 （或数据） 的单独部分，有时可能可分页，但有时必须锁定到隔离纯粹可分页的代码 （或数据）。 例如，组合可分页纯代码和按需锁定代码会导致更多的系统空间锁定组合部分不必要。 但是，如果驱动程序包含小于 4 KB 的可能是可分页代码 （或数据），可能会合并锁定根据代码 （或数据） 到一个部分中，将保存系统空间的该代码 （或数据）。

 

 




