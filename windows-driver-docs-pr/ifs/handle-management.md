---
title: 句柄管理
description: 句柄管理
keywords:
- 处理 WDK 文件系统
- 安全 WDK 文件系统，最大限度地减少威胁
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 520d225b5eeff0cd21d770abac2d26f54f74a863
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814445"
---
# <a name="handle-management"></a>句柄管理


## <span id="ddk_handle_management_if"></span><span id="DDK_HANDLE_MANAGEMENT_IF"></span>


驱动程序中的重要安全问题源是使用在用户模式和内核模式组件之间传递的句柄。 内核环境中存在一些处理使用情况的已知问题，包括以下各项：

-   向内核驱动程序传递错误类型的句柄的应用程序。 内核驱动程序在尝试使用需要文件对象的事件对象时可能会崩溃。

-   一种应用程序，它将句柄传递给它没有必要的访问权限的对象。 内核驱动程序可能会执行工作，因为调用来自内核模式，即使用户没有足够的权限来执行此操作。

-   一种应用程序，该应用程序在其地址空间中传递的值不是有效的句柄，但被标记为系统句柄，以对系统执行恶意操作。

-   一种应用程序，该应用程序传递的值不是此驱动程序未创建) 的句柄的设备 (对象的合适句柄。

若要防止这些问题，内核驱动程序必须特别注意，以确保传递给它的句柄有效。 最安全的策略是在驱动程序的上下文中创建任何所需的句柄。 这些由内核驱动程序创建的句柄应指定 OBJ \_ 内核 \_ 句柄选项，该选项将创建一个在任意进程上下文中有效的句柄，以及一个只能从内核模式调用方访问的句柄。

对于使用由应用程序创建的句柄的驱动程序，必须特别小心地使用这些句柄：

-   最佳做法是通过调用 [**ObReferenceObjectByHandle**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)将句柄转换为对象指针，并指定通常来自 Irp *AccessMode* - &gt; Irp->requestormode) 、 *DesiredAccess* 和 *ObjectType* 参数（如 IoFileObjectType 或 ExEventObjectType）的正确 AccessMode (。

-   如果句柄必须直接在调用中使用，则最好使用函数的 Nt 变体，而不是函数的 Zw 变体。 这会强制执行参数检查并处理操作系统验证，因为上一模式将为 **UserMode** ，因此不受信任。 请注意，如果先前模式为 **UserMode**，则传递到作为指针的 Nt 函数的参数可能无法通过验证。 Nt 和 Zw 例程返回应检查错误的 *IoStatusBlock* parameterwith 错误信息。

-   如果需要，还必须使用 \_ \_ try 和 except 来适当地捕获错误 \_ \_ 。 许多缓存管理器 (Cc) 、内存管理器 (Mm) 以及文件系统运行时库例程 (FsRtl) 发生错误时引发异常。

任何驱动程序都不应依赖于从用户模式应用程序传递的句柄或参数，而无需采取适当的措施。

请注意，如果使用 Nt 变量打开文件，则还必须使用 Nt 变体关闭文件。

 

