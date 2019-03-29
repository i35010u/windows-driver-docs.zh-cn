---
title: 框架对象集合
description: 框架对象集合
ms.assetid: e3f29be6-ee4c-487a-8c85-18be8b6a5cdc
keywords:
- framework 对象 WDK KMDF，集合
- 集合 WDK KMDF
- framework 的集合对象 WDK KMDF
- 对象集合 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcd405f43bfe91a7154eadf1decf198a09ec88d5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565740"
---
# <a name="framework-object-collections"></a>框架对象集合





驱动程序可以分组到由表示的集合的 framework 对象*framework 集合对象*。

例如，如果驱动程序收到一个表示大型 I/O 请求的框架请求对象，该驱动程序可能需要分解为较小请求，它可以发送到的大型请求[I/O 目标](using-i-o-targets.md)。 若要分解为较小的大型请求，该驱动程序必须创建一组表示较小的请求的请求对象。 若要跟踪的这些驱动程序创建请求对象，该驱动程序可能创建集合对象并将它们添加到集合。

通常情况下，对象集合中的对象包含单一类型的 framework 对象，但驱动程序可以创建一个集合，其中包含不同类型的对象。

您的驱动程序还可以创建集合的集合。 也就是说，集合可以包含一组的集合对象。

基于框架的驱动程序可以执行对对象的集合执行以下操作：

-   创建集合对象。

    若要创建新的集合，驱动程序可以调用[ **WdfCollectionCreate**](https://msdn.microsoft.com/library/windows/hardware/ff545747)。

-   将对象添加到集合。

    若要将对象添加到集合中，驱动程序可以调用[ **WdfCollectionAdd**](https://msdn.microsoft.com/library/windows/hardware/ff545732)、 一个或多个时间。 每次调用**WdfCollectionAdd**将对象追加到集合的末尾并追加的对象的引用计数会递增。

-   从集合中移除一个对象。

    若要从集合中移除一个对象，并减少其引用计数，驱动程序可以调用[ **WdfCollectionRemove** ](https://msdn.microsoft.com/library/windows/hardware/ff545784)或[ **WdfCollectionRemoveItem**](https://msdn.microsoft.com/library/windows/hardware/ff545792). 删除对象后之后删除, 的所有对象都具有其索引自动减少。

-   获取集合中的对象数。

    若要确定集合中包含的对象数，驱动程序可以调用[ **WdfCollectionGetCount**](https://msdn.microsoft.com/library/windows/hardware/ff545759)。

-   获取集合中对象的句柄。

    如果驱动程序调用[ **WdfCollectionGetItem**](https://msdn.microsoft.com/library/windows/hardware/ff545770)，提供的索引值作为输入参数，驱动程序收到的句柄的索引值与相关联的对象。 （的索引值为零表示集合中的第一个对象的索引值为 1 表示第二个对象，依次类推-如链接列表。 当驱动程序移除项*我*集合中项*我*+ 1 将成为项*我*。)

    驱动程序还可以调用[ **WdfCollectionGetFirstItem** ](https://msdn.microsoft.com/library/windows/hardware/ff545763)或[ **WdfCollectionGetLastItem** ](https://msdn.microsoft.com/library/windows/hardware/ff545775)若要获取的句柄的第一个或最后一个项已添加到集合。

-   锁定集合。

    驱动程序可以调用[ **WdfWaitLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff551168)同步访问集合中的 IRQL = 被动\_级别，也可以调用[ **WdfSpinLockAcquire**](https://msdn.microsoft.com/library/windows/hardware/ff550040)同步访问在 IRQL = 调度\_级别。 驱动程序将获取的锁后，还会调用该驱动程序中的其他代码不能访问集合**WdfWaitLockAcquire**或**WdfSpinLockAcquire**。 完成后对集合的操作，该驱动程序必须调用[ **WdfWaitLockRelease**](https://msdn.microsoft.com/library/windows/hardware/ff551173)。

    调用[ **WdfWaitLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff551168)或[ **WdfSpinLockAcquire** ](https://msdn.microsoft.com/library/windows/hardware/ff550040)同时不会阻止从驱动程序中的其他代码访问集合中，如果其他代码不会还调用**WdfWaitLockAcquire**或**WdfSpinLockAcquire**。

-   删除集合。

    若要删除的集合对象，驱动程序可以调用[ **WdfObjectDelete**](https://msdn.microsoft.com/library/windows/hardware/ff548734)。 更常见的做法，但是，驱动程序指定父对象时在创建集合，并删除父对象时，框架将删除的集合对象。

    例如，如果驱动程序创建一组请求对象，以便它可以将大型 I/O 请求分为较小的请求，它可以发出大型 I/O 请求的请求对象的集合对象的父对象。 驱动程序的 I/O 目标将调用最终[ **WdfRequestComplete** ](https://msdn.microsoft.com/library/windows/hardware/ff549945)来完成较小的请求。 此时，驱动程序可以调用**WdfRequestComplete**大型 I/O 请求，从而导致删除请求对象，它的子对象的框架： 集合对象。

    当集合对象，包含对象尚未删除 framework 删除操作的情况下，框架将删除从对象的集合和递减及其引用计数，但会删除仅的集合对象。

有时一个驱动程序必须检查所有集合中的对象。 下面的代码示例演示了这种情况：

```cpp
WdfWaitLockAcquire(CollectionLockHandle, NULL);
ItemCount = WdfCollectionGetCount(CollectionHandle);
for (i=0; i<ItemCount; i++) {
    ObjectHandle = WdfCollectionGetItem(CollectionHandle, i);
    // 1. Call object-specific methods to obtain object properties.
    // 2. Perform object-specific operations.
    }
WdfWaitLockRelease(CollectionLockHandle);
```

 

 





