---
title: 对象的包
description: 对象的包
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
ms.openlocfilehash: 59000e54a1b35e33d382fdeaae7ad943ded5232e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547172"
---
# <a name="object-bags"></a>对象的包





AVStream 管理称为微型驱动程序可以看到每个 AVStream 对象对象包的构造。 对象包是一个通用容器用于保存动态分配的内存与给定对象相关联。

以下结构具有成员类型 KSOBJECT\_袋，这相当于 PVOID:[**KSDEVICE**](https://msdn.microsoft.com/library/windows/hardware/ff561681)， [ **KSFILTERFACTORY**](https://msdn.microsoft.com/library/windows/hardware/ff562530)， [ **KSFILTER**](https://msdn.microsoft.com/library/windows/hardware/ff562522)，和[ **KSPIN**](https://msdn.microsoft.com/library/windows/hardware/ff563483)。

对象包的用途包括：

-   内存管理。

    微型驱动程序可以使用内存管理对象的包以减少清理工作。 若要执行此操作，微型驱动程序首先必须调用[ **ExAllocatePoolWithTag** ](https://msdn.microsoft.com/library/windows/hardware/ff544520)分配动态内存，并将其与给定的对象相关联。 微型驱动程序然后将添加已分配的内存对象包到通过调用[ **KsAddItemToObjectBag**](https://msdn.microsoft.com/library/windows/hardware/ff560941)。

    当调用微型驱动程序**KsAddItemToObjectBag**，AVStream 将默认清理函数相关联 (通常[ **ExFreePool**](https://msdn.microsoft.com/library/windows/hardware/ff544590)) 与对象。 或者，微型驱动程序可以包含指向中的微型驱动程序提供清理例程的指针*免费*的参数**KsAddItemToObjectBag**。 当对象已关闭时，AVStream 从对象包中删除的每个项，并调用相关联的清理例程。

-   动态共享分配多个 AVStream 对象之间的数据。

    微型驱动程序可以通过将给定的项放入多个对象的包共享 AVStream 的多个对象之间动态分配的数据。 在这种情况下，AVStream 不会释放给定的项，直到其不再包含任何对象包中。 在对象包可包含的项数的唯一限制是可用内存。

-   确定哪个结构可以使用描述符进行编辑。

    如果微型驱动程序动态分配一个描述符或描述符子结构，微型驱动程序将包中的相关对象的描述符。 [  **\_KsEdit** ](https://msdn.microsoft.com/library/windows/hardware/ff568796)函数然后使用此信息来确定是否可以编辑给定的结构。

AVStream 自动从移除项对象包如果删除所属的对象。

微型驱动程序可以各项从包中取出对象通过调用[ **KsRemoveItemFromObjectBag** ](https://msdn.microsoft.com/library/windows/hardware/ff566798)或[ **KsDiscard**](https://msdn.microsoft.com/library/windows/hardware/ff561695)。

 

 




