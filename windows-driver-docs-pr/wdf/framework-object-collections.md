---
title: 框架对象集合
description: 框架对象集合
ms.assetid: e3f29be6-ee4c-487a-8c85-18be8b6a5cdc
keywords:
- framework 对象 WDK KMDF、集合
- 集合 WDK KMDF
- 框架集合对象 WDK KMDF
- 对象集合 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ead2c00ce24a40be79a1d988ac4c32c931f34a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72823702"
---
# <a name="framework-object-collections"></a>框架对象集合





驱动程序可以将框架对象分组到由*框架集合对象*表示的集合中。

例如，如果驱动程序收到一个表示大型 i/o 请求的 framework 请求对象，则驱动程序可能需要将大型请求拆分为可发送到[i/o 目标](using-i-o-targets.md)的小型请求。 若要将大请求拆分为较小的请求，驱动程序必须创建一组表示较小请求的请求对象。 为了跟踪这些驱动程序创建的请求对象，驱动程序可能会创建集合对象并将其添加到集合中。

通常，对象集合中的对象包含一类框架对象，但驱动程序可以创建一个包含不同类型的对象的集合。

你的驱动程序还可以创建集合的集合。 也就是说，集合可以包含一组集合对象。

基于框架的驱动程序可以对对象集合执行以下操作：

-   创建集合对象。

    若要创建新集合，驱动程序可以调用[**WdfCollectionCreate**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectioncreate)。

-   将对象添加到集合。

    若要将对象添加到集合中，驱动程序可以调用[**WdfCollectionAdd**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectionadd)，一次或多次。 对**WdfCollectionAdd**的每次调用都会将一个对象追加到集合的末尾，并递增追加的对象的引用计数。

-   从集合中删除对象。

    若要从集合中删除对象并减小其引用计数，驱动程序可以调用[**WdfCollectionRemove**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectionremove)或[**WdfCollectionRemoveItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectionremoveitem)。 删除对象后，删除后的所有对象都将自动减少其索引。

-   获取集合中的对象数。

    若要确定集合包含的对象数，驱动程序可以调用[**WdfCollectionGetCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectiongetcount)。

-   获取集合中对象的句柄。

    如果驱动程序调用[**WdfCollectionGetItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectiongetitem)，将索引值提供为输入参数，则驱动程序将接收与索引值相关联的对象的句柄。 （如果索引值为零，则表示集合中的第一个对象，索引值为1表示第二个对象，依此类推，如链接列表。 当驱动程序从集合中删除项*i*时，项*i*+ 1 成为项*i*。）

    驱动程序还可以调用[**WdfCollectionGetFirstItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectiongetfirstitem)或[**WdfCollectionGetLastItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfcollection/nf-wdfcollection-wdfcollectiongetlastitem)来获取已添加到集合中的第一个或最后一个项的句柄。

-   锁定集合。

    驱动程序可以调用[**WdfWaitLockAcquire**](https://msdn.microsoft.com/library/windows/hardware/ff551168)来同步对集合的访问（IRQL = 被动\_级别），也可以调用[**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85)) synchronize =\_级别的同步访问。 驱动程序获取锁定后，也将调用**WdfWaitLockAcquire**或**WdfSpinLockAcquire**的驱动程序中的其他代码不能访问该集合。 完成对集合的操作之后，驱动程序必须调用[**WdfWaitLockRelease**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfsync/nf-wdfsync-wdfwaitlockrelease)。

    如果其他代码还没有调用**WdfWaitLockAcquire**或**WdfSpinLockAcquire**，则调用[**WdfWaitLockAcquire**](https://msdn.microsoft.com/library/windows/hardware/ff551168)或[**WdfSpinLockAcquire**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff550040(v=vs.85))不会阻止驱动程序中的其他代码同时访问该集合。

-   删除集合。

    若要删除集合对象，驱动程序可以调用[**WdfObjectDelete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete)。 然而，通常情况下，驱动程序在创建集合时指定了父对象，框架在删除父对象时删除了集合对象。

    例如，如果驱动程序创建一组请求对象，以便它可以将较大的 i/o 请求拆分为较小的请求，则它可以使大型 i/o 请求的 request 对象成为 collection 对象的父对象。 最终，驱动程序的 i/o 目标将调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)来完成较小的请求。 此时，驱动程序可以调用**WdfRequestComplete**来执行大型 i/o 请求，从而使框架删除请求对象及其子对象：集合对象。

    当框架删除包含尚未删除的对象的集合对象时，框架将从集合中删除这些对象并减小其引用计数，但它仅删除集合对象。

有时，驱动程序必须检查集合中的所有对象。 下面的代码示例演示了这种情况：

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

 

 





