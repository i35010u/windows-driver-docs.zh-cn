---
title: 对象包
description: 对象包
ms.assetid: b7ee5756-1c79-4ead-9999-d13be9a0d3d9
keywords:
- AVStream 对象包 WDK
- 对象包 WDK AVStream
- WDK AVStream 对象
- 内存管理 WDK AVStream
- 动态共享为 AVStream WDK 分配数据
- 动态分配数据 WDK AVStream
- AVStream 描述符 WDK
- 描述符 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c7d35628bd23d5f87dc3db0fc9dcbc799a9c035d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67377516"
---
# <a name="object-bags"></a>对象包





AVStream 管理称为微型驱动程序可以看到每个 AVStream 对象对象包的构造。 对象包是一个通用容器用于保存动态分配的内存与给定对象相关联。

以下结构具有成员类型 KSOBJECT\_袋，这相当于 PVOID:[**KSDEVICE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice)， [ **KSFILTERFACTORY**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilterfactory)， [ **KSFILTER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksfilter)，和[ **KSPIN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_kspin)。

对象包的用途包括：

-   内存管理。

    微型驱动程序可以使用内存管理对象的包以减少清理工作。 若要执行此操作，微型驱动程序首先必须调用[ **ExAllocatePoolWithTag** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exallocatepoolwithtag)分配动态内存，并将其与给定的对象相关联。 微型驱动程序然后将添加已分配的内存对象包到通过调用[ **KsAddItemToObjectBag**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksadditemtoobjectbag)。

    当调用微型驱动程序**KsAddItemToObjectBag**，AVStream 将默认清理函数相关联 (通常[ **ExFreePool**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddk/nf-ntddk-exfreepool)) 与对象。 或者，微型驱动程序可以包含指向中的微型驱动程序提供清理例程的指针*免费*的参数**KsAddItemToObjectBag**。 当对象已关闭时，AVStream 从对象包中删除的每个项，并调用相关联的清理例程。

-   动态共享分配多个 AVStream 对象之间的数据。

    微型驱动程序可以通过将给定的项放入多个对象的包共享 AVStream 的多个对象之间动态分配的数据。 在这种情况下，AVStream 不会释放给定的项，直到其不再包含任何对象包中。 在对象包可包含的项数的唯一限制是可用内存。

-   确定哪个结构可以使用描述符进行编辑。

    如果微型驱动程序动态分配一个描述符或描述符子结构，微型驱动程序将包中的相关对象的描述符。 [  **\_KsEdit** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-_ksedit)函数然后使用此信息来确定是否可以编辑给定的结构。

AVStream 自动从移除项对象包如果删除所属的对象。

微型驱动程序可以各项从包中取出对象通过调用[ **KsRemoveItemFromObjectBag** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksremoveitemfromobjectbag)或[ **KsDiscard**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/nf-ks-ksdiscard)。

 

 




