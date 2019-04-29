---
title: 句柄管理
description: 句柄管理
ms.assetid: 09d9c836-1754-4a50-92a3-229a3ae05ccb
keywords:
- 处理 WDK 的文件系统
- 安全 WDK 文件系统、 最大程度减少威胁
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0845ab39acdb99bf15bce48f5714355f8d924339
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63370135"
---
# <a name="handle-management"></a>句柄管理


## <span id="ddk_handle_management_if"></span><span id="DDK_HANDLE_MANAGEMENT_IF"></span>


驱动程序中的安全问题的重要源是使用用户模式和内核模式组件之间传递的句柄。 有许多与句柄使用内核环境中，其中包括以下已知问题：

-   将错误类型的句柄传递给内核驱动程序应用程序。 内核驱动程序可能会崩溃尝试使用一个事件对象需要文件对象的位置。

-   将传递一个句柄到对象，它不具有所需访问应用程序。 内核驱动程序可能执行的操作有效，因为调用是来自内核模式下，即使用户没有足够的权限执行此操作。

-   将值传递的应用程序不是有效的句柄中其地址空间，但却标记为系统句柄来执行针对系统的恶意操作。

-   将值传递应用程序不是合适的句柄的设备对象 （此驱动程序未创建句柄）。

若要避免出现这些问题，内核驱动程序必须特别小心，以确保有效句柄传递给它。 最安全的策略是创建驱动程序的上下文中任何所需的句柄。 这些句柄，由内核驱动程序，应指定 OBJ\_内核\_句柄选项，将创建一个句柄有效中任意进程上下文，仅可以从内核模式调用方访问的一个。

可以使用句柄创建的应用程序的驱动程序，请使用这些句柄必须小心地使用完成操作：

-   最佳做法是将该句柄转换为一个对象指针，通过调用[ **ObReferenceObjectByHandle**](https://msdn.microsoft.com/library/windows/hardware/ff558679)，指定正确*AccessMode* （通常从 Irp&gt;RequestorMode)， *DesiredAccess*，并*ObjectType*参数，例如 IoFileObjectType 或 ExEventObjectType。

-   如果必须直接在调用中使用一个句柄，则最好使用函数的 Nt 变量而不是函数的 Zw 变量。 这将由操作系统强制参数检查和句柄验证，因为以前的模式会**UserMode**并因此不受信任。 请注意参数传递给 Nt 函数的指针可能会失败的验证，如果上一个模式，则**UserMode**。 Nt 和 Zw 例程将返回*IoStatusBlock* parameterwith 应检查是否有错误的错误信息。

-   必须相应地捕获错误以及使用\_\_尝试并\_\_在必要时除外。 发生错误时，许多缓存管理器 (Cc)、 内存管理器 (Mm) 和文件系统运行时库例程 (FsRtl) 引发一个异常。

没有驱动程序应曾经依赖句柄或不采取适当的预防措施，直接从用户模式应用程序传递参数。

请注意，是否 Nt 变体用于打开文件，然后 Nt 变体必须也用于关闭该文件。

 

 




