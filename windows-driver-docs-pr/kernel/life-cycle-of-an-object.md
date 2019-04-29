---
title: 对象的生命周期
description: 对象的生命周期
ms.assetid: e81bfce6-27c4-4916-adc8-9c014d02bee7
keywords:
- 对象生命周期 WDK 内核
- 生命周期 WDK 对象
- 引用对象
- 对象的引用计数 WDK 内核
- 临时对象 WDK 内核
- 永久对象 WDK 内核
- 引用计数 WDK 对象
- 已释放的对象 WDK 内核
- 对象临时状态 WDK 内核
- 对象永久状态 WDK 内核
- 自动对象删除 WDK 内核
- 对象跟踪 WDK 内核
- 打开对象句柄 WDK 内核
- 计数 WDK 对象的引用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ee77d2900138b800722496dd6c4cc3128f6f295
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381367"
---
# <a name="life-cycle-of-an-object"></a>对象的生命周期





本主题描述一个对象，它的"生命周期"，如何引用和跟踪的对象管理器对象。 本主题还介绍如何临时或永久对象。

### <a name="object-reference-count"></a>对象引用计数

对象管理器维护的引用的对象数的计数。 当创建一个对象时，对象管理器对象的引用计数设置为 1。 一旦该计数器降到零时，会释放该对象。

驱动程序必须确保对象管理器具有它们操作的任何对象的准确的引用计数。 过早地释放的对象可能会导致系统崩溃。 一个对象，其引用计数是错误地高永远不会被释放。

句柄或指针，则可以引用对象。 除了引用计数对象管理器维护打开的句柄的对象数的计数。 每个打开句柄的例程会对象引用计数和对象句柄计数增加 1。 每次调用此类例程必须与相应地调用匹配[ **ZwClose**](https://msdn.microsoft.com/library/windows/hardware/ff566417)。 有关详细信息，请参阅[对象处理](object-handles.md)。

在内核模式下，可以通过指向对象的引用对象。 返回指向对象，如的例程[ **IoGetAttachedDeviceReference**](https://msdn.microsoft.com/library/windows/hardware/ff549145)，引用计数增加 1。 该驱动程序完成后使用指针，它必须调用[ **ObDereferenceObject** ](https://msdn.microsoft.com/library/windows/hardware/ff557724)以引用计数减少 1。

下面的例程所有对象的引用计数都增加一：

[**ExCreateCallback**](https://msdn.microsoft.com/library/windows/hardware/ff544560)

[**IoGetAttachedDeviceReference**](https://msdn.microsoft.com/library/windows/hardware/ff549145)

[**IoGetDeviceObjectPointer**](https://msdn.microsoft.com/library/windows/hardware/ff549198)

[**IoWMIOpenBlock**](https://msdn.microsoft.com/library/windows/hardware/ff550453)

[**ObReferenceObject**](https://msdn.microsoft.com/library/windows/hardware/ff558678)

[**ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)

[**ObReferenceObjectByPointer**](https://msdn.microsoft.com/library/windows/hardware/ff558686)

对任何上述例程进行每次调用必须匹配与相应地调用**ObDereferenceObject**。

**ObReferenceObject**并**ObReferenceObjectByPointer**例程提供，以便驱动程序可以增加的已知的对象指针的引用计数 1。 **ObReferenceObject**只需增加引用计数。 **ObReferenceObjectByPointer**执行访问检查之前增加引用计数。

**ObReferenceObjectByHandle**例程接收对象句柄，并提供指向基础对象的指针。 它也使引用计数加一。

### <a name="temporary-and-permanent-objects"></a>临时和永久对象

大多数对象都是*临时*; 它们存在，只要他们正在使用，并且对象管理器然后释放。 可创建对象的*永久*。 如果对象是永久性的对象管理器本身保存对该对象的引用。 因此，其引用计数大于零，并且不再使用时不会释放该对象。

可以通过名称访问的临时对象，仅当其句柄计数为非零值。 一旦句柄计数递减到零，对象的名称已从对象管理器的命名空间。 只要其引用计数保持大于零，则仍可以通过指针访问此类对象。 可以通过名称访问的永久对象，因为它们存在。

对象可以通过永久在其创建时指定 OBJ\_中的永久属性[**对象\_特性**](https://msdn.microsoft.com/library/windows/hardware/ff557749)对象的结构。 有关详细信息，请参阅[ **InitializeObjectAttributes**](https://msdn.microsoft.com/library/windows/hardware/ff547804)。

若要进行临时永久对象，使用[ **ZwMakeTemporaryObject** ](https://msdn.microsoft.com/library/windows/hardware/ff566477)例程。 此例程会导致对象无法再使用后自动删除。 （如果该对象具有打开的句柄，该对象的名称将立即删除从对象管理器的命名空间。 对象本身将保持直到引用计数降为零。）

 

 




