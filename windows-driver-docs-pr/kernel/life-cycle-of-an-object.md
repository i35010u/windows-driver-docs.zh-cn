---
title: 对象的生命周期
description: 对象的生命周期
ms.assetid: e81bfce6-27c4-4916-adc8-9c014d02bee7
keywords:
- 对象生命周期 WDK 内核
- 生命周期 WDK 对象
- 引用对象
- 对象引用计数 WDK 内核
- 临时对象 WDK 内核
- 永久对象 WDK 内核
- 引用计数 WDK 对象
- 已释放对象 WDK 内核
- 对象临时状态 WDK 内核
- 对象永久状态 WDK 内核
- 自动对象删除 WDK 内核
- 对象跟踪 WDK 内核
- 开放式对象处理 WDK 内核
- 统计引用 WDK 对象
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 807f6d1406cfbd3dd0fba0809a30b0fd4a39c5f5
ms.sourcegitcommit: a5f76805387760730faed5674d87201ec85b7dd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90112096"
---
# <a name="life-cycle-of-an-object"></a>对象的生命周期





本主题介绍对象的 "生命周期"，即对象管理器引用和跟踪对象的方式。 本主题还介绍如何将对象设为临时或永久。

### <a name="object-reference-count"></a>对象引用计数

对象管理器维护对对象的引用数的计数。 当创建对象时，对象管理器将对象的引用计数设置为1。 一旦该计数器降为零，就会释放该对象。

驱动程序必须确保对象管理器对其操作的任何对象都具有准确的引用计数。 提前发布的对象可能会导致系统崩溃。 不会释放其引用计数过高的对象。

可以通过句柄或指针来引用对象。 除引用计数外，对象管理器还维持对象的打开句柄数的计数。 打开一个句柄的每个例程都会同时增加对象引用计数和对象句柄计数。 对此类例程的每个调用都必须与相应的 [**ZwClose**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntclose)调用匹配。 有关详细信息，请参阅 [对象句柄](object-handles.md)。

在内核模式下，对象可以由指向对象的指针引用。 返回指向对象的指针的例程（如 [**IoGetAttachedDeviceReference**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)）会将引用计数增加一。 使用指针完成驱动程序后，它必须调用 [**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject) ，将引用计数减少1。

以下例程会按1增加对象的引用计数：

[**ExCreateCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)

[**IoGetAttachedDeviceReference**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iogetattacheddevicereference)

[**Plxntb**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceobjectpointer)

[**IoWMIOpenBlock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iowmiopenblock)

[**ObReferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)

[**ObReferenceObjectByHandle**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)

[**ObReferenceObjectByPointer**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbypointer)

对上述任何例程进行的每个调用都必须与相应的 **ObDereferenceObject**调用匹配。

提供了 **ObReferenceObject** 和 **ObReferenceObjectByPointer** 例程，以便驱动程序可以将已知对象指针的引用计数增加一。 **ObReferenceObject** 只会增加引用计数。 在增大引用计数之前， **ObReferenceObjectByPointer**执行访问检查。

**ObReferenceObjectByHandle**例程接收对象句柄，并提供指向基础对象的指针。 它也会将引用计数增加一。

### <a name="temporary-and-permanent-objects"></a>临时和永久对象

大多数对象都是 *临时*的;它们存在，只要它们处于使用中，就会被对象管理器释放。 可以创建 *永久*的对象。 如果对象是永久性的，则对象管理器本身将保留对该对象的引用。 因此，其引用计数保持大于零，并且对象在不再使用时不会被释放。

临时对象只能通过名称进行访问，只要其句柄计数不为零。 句柄计数减为零时，会从对象管理器的命名空间中删除该对象的名称。 此类对象的引用计数保持大于零时，仍然可以通过指针访问此类对象。 可以通过名称访问永久对象，只要这些对象存在。

在创建对象时，可以通过在对象 \_ 的 [**对象 \_ 属性**](/windows/win32/api/ntdef/ns-ntdef-_object_attributes) 结构中指定 OBJ 永久属性，使该对象成为永久属性。 有关详细信息，请参阅 [**InitializeObjectAttributes**](/windows/win32/api/ntdef/nf-ntdef-initializeobjectattributes)。

若要使永久对象成为临时对象，请使用 [**ZwMakeTemporaryObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwmaketemporaryobject) 例程。 此例程会使对象在不再使用后被自动删除。  (如果对象没有打开的句柄，则会立即从对象管理器的命名空间中删除该对象的名称。 对象本身仍保留，直到引用计数降为零。 ) 

 

