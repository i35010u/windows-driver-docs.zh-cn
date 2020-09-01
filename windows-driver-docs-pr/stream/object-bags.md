---
title: 对象包
description: 对象包
ms.assetid: b7ee5756-1c79-4ead-9999-d13be9a0d3d9
keywords:
- AVStream 对象包 WDK
- 对象包 WDK AVStream
- 对象 WDK AVStream
- 内存管理 WDK AVStream
- 共享 AVStream WDK 的动态分配的数据
- 动态分配的数据 WDK AVStream
- AVStream 描述符 WDK
- 描述符 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d27a0a1a0264d12b7e5abcb2da790edcdfd7e9b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89192141"
---
# <a name="object-bags"></a>对象包





AVStream 管理被称为对象包的构造，这些 AVStream 对象对微型驱动程序可见。 对象包是用于保存与给定对象关联的动态分配的内存的泛型容器。

以下结构具有类型为 KSOBJECT 包的成员 \_ ，它等效于 PVOID： [**KSDEVICE**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice)、 [**KSFILTERFACTORY**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilterfactory)、 [**KSFILTER**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter)和 [**KSPIN**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin)。

对象包的用途包括：

-   内存管理。

    微型驱动程序可以使用对象包进行内存管理，以减少清理工作。 若要执行此操作，微型驱动程序必须首先调用 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 来分配动态内存，并将其与给定的对象相关联。 然后，微型驱动程序通过调用 [**KsAddItemToObjectBag**](/windows-hardware/drivers/ddi/ks/nf-ks-ksadditemtoobjectbag)将分配的内存添加到对象包。

    当微型驱动程序调用 **KsAddItemToObjectBag**时，AVStream 会将默认清理函数 [** (通常) **](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool) 与对象相关联。 或者，微型驱动程序可以在**KsAddItemToObjectBag**的*Free*参数中包含指向微型驱动程序提供的清理例程的指针。 关闭对象时，AVStream 会从对象包中移除每个项并调用关联的清理例程。

-   在多个 AVStream 对象之间共享动态分配的数据。

    微型驱动程序可以通过在多个对象包中放置给定项来共享多个 AVStream 对象之间的动态分配的数据。 在这种情况下，AVStream 不会释放给定的项，直到该项不再包含在任何对象包中为止。 对象包可以包含的项目数的唯一限制是可用内存。

-   确定可通过描述符编辑的结构。

    如果微型驱动程序动态分配描述符或描述符子结构，则微型驱动程序会将描述符放在相关的对象包中。 然后， [** \_ KsEdit**](/windows-hardware/drivers/ddi/ks/nf-ks-_ksedit)函数将使用此信息来确定是否可以编辑给定的结构。

如果删除了所属对象，AVStream 会自动从对象包中删除项目。

微型驱动程序可以通过调用 [**KsRemoveItemFromObjectBag**](/windows-hardware/drivers/ddi/ks/nf-ks-ksremoveitemfromobjectbag) 或 [**KsDiscard**](/windows-hardware/drivers/ddi/ks/nf-ks-ksdiscard)删除对象包中的单个项。

 

