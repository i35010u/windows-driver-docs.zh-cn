---
title: 句柄管理
description: 句柄管理
ms.assetid: 09d9c836-1754-4a50-92a3-229a3ae05ccb
keywords:
- 处理 WDK 文件系统
- 安全 WDK 文件系统，最大限度地减少威胁
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6d70f7573d6172ba275aa028eaf6be077253587
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841223"
---
# <a name="handle-management"></a>句柄管理


## <span id="ddk_handle_management_if"></span><span id="DDK_HANDLE_MANAGEMENT_IF"></span>


驱动程序中的重要安全问题源是使用在用户模式和内核模式组件之间传递的句柄。 内核环境中存在一些处理使用情况的已知问题，包括以下各项：

-   向内核驱动程序传递错误类型的句柄的应用程序。 内核驱动程序在尝试使用需要文件对象的事件对象时可能会崩溃。

-   一种应用程序，它将句柄传递给它没有必要的访问权限的对象。 内核驱动程序可能会执行工作，因为调用来自内核模式，即使用户没有足够的权限来执行此操作。

-   一种应用程序，该应用程序在其地址空间中传递的值不是有效的句柄，但被标记为系统句柄，以对系统执行恶意操作。

-   一种应用程序，该应用程序传递的值不是设备对象（此驱动程序未创建的句柄）的合适句柄。

若要防止这些问题，内核驱动程序必须特别注意，以确保传递给它的句柄有效。 最安全的策略是在驱动程序的上下文中创建任何所需的句柄。 这些由内核驱动程序创建的句柄应指定 OBJ\_内核\_句柄选项，这将创建一个在任意进程上下文中有效的句柄，以及一个只能从内核模式调用方访问的句柄。

对于使用由应用程序创建的句柄的驱动程序，必须特别小心地使用这些句柄：

-   最佳做法是通过调用[**ObReferenceObjectByHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obreferenceobjectbyhandle)将句柄转换为对象指针，并指定正确的*AccessMode* （通常从 Irp&gt;irp->requestormode）、 *DesiredAccess*和*ObjectType*参数，如 IoFileObjectType 或 ExEventObjectType。

-   如果句柄必须直接在调用中使用，则最好使用函数的 Nt 变体，而不是函数的 Zw 变体。 这会强制执行参数检查并处理操作系统验证，因为上一模式将为**UserMode** ，因此不受信任。 请注意，如果先前模式为**UserMode**，则传递到作为指针的 Nt 函数的参数可能无法通过验证。 Nt 和 Zw 例程返回应检查错误的*IoStatusBlock* parameterwith 错误信息。

-   使用 \_\_尝试并 \_\_时，必须适当地捕获错误，除非必要。 许多缓存管理器（Cc）、内存管理器（Mm）和文件系统运行时库例程（FsRtl）在发生错误时引发异常。

任何驱动程序都不应依赖于从用户模式应用程序传递的句柄或参数，而无需采取适当的措施。

请注意，如果使用 Nt 变量打开文件，则还必须使用 Nt 变体关闭文件。

 

 




