---
title: 什么是驱动程序？
description: 什么是驱动程序？
keywords:
- 定义驱动程序
- 驱动程序定义
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f1e58bdc66bb0d6555f1daada8bb06473d715f8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786327"
---
# <a name="what-is-a-driver"></a>什么是驱动程序？


为术语 *驱动程序* 给出单一的准确定义比较困难。 就最基本的意义而言，驱动程序是一个软件组件，可让操作系统和设备彼此通信。 例如，假设应用程序需要从设备中读取某些数据。 应用程序会调用由操作系统实现的函数，操作系统会调用由驱动程序实现的函数。 驱动程序（由设计和制造该设备的同一公司编写）了解如何与设备硬件通信以获取数据。 当驱动程序从设备获取数据后，它会将数据返回到操作系统，操作系统会将数据返回至应用程序。

![图：显示应用程序、操作系统以及驱动程序](images/whatisadriver01.png)

## <a name="span-idexpanding_the_definitionspanspan-idexpanding_the_definitionspanspan-idexpanding_the_definitionspanexpanding-the-definition"></a><span id="Expanding_the_definition"></span><span id="expanding_the_definition"></span><span id="EXPANDING_THE_DEFINITION"></span>扩展定义


到目前为止，我们的说明在几个方面过于简单化：

-   并非所有驱动程序都必须由设计该设备的公司编写。 在许多情况下，设备是根据已发布的硬件标准进行设计的。 这意味着驱动程序可以由 Microsoft 编写，设备设计者无须提供驱动程序。

-   并非所有驱动程序都直接与设备通信。 对于给定的 I/O 请求（如从设备读取数据），通常有一些驱动程序（在堆栈中进行分层）参与该请求。 将堆栈可视化的常规方法是将第一个参与对象放在顶部，将最后一个参与对象放在底部，如此图所示。 堆栈中的某些驱动程序可能通过将请求从一种格式转换为另一种格式来参与。 这些驱动程序不直接与设备通信；它们只是操纵请求并将请求传递给堆栈中较低的驱动程序。

    ![图：显示应用程序、操作系统、3 个驱动程序以及设备](images/whatisadriver02.png)

    堆栈中直接与设备通信的一个驱动程序称为“函数驱动程序”  ；执行辅助处理的驱动程序称为“筛选器驱动程序”  。

-   某些筛选器驱动程序观察并记录有关 I/O 请求的信息，但不会主动参与这些请求。 例如，某些筛选器驱动程序充当验证程序以确保堆栈中的其他驱动程序正确处理 I/O 请求。

我们可以扩展驱动程序  的定义，即驱动程序是观察或参与操作系统和设备之间通信的任何软件组件。

## <a name="span-idsoftware_driversspanspan-idsoftware_driversspanspan-idsoftware_driversspansoftware-drivers"></a><span id="Software_drivers"></span><span id="software_drivers"></span><span id="SOFTWARE_DRIVERS"></span>软件驱动程序


我们的扩展定义相当准确，但仍然不完整，因为有些驱动程序根本不与任何硬件设备相关联。 例如，假设你需要编写可以访问核心操作系统数据结构的工具，这些结构仅可以由内核模式下运行的代码进行访问。 可以通过将工具拆分成两个组件来执行该操作。 第一个组件在用户模式下运行且提供用户界面。 第二个组件在内核模式下运行且可以访问核心操作系统数据。 在用户模式下运行的组件称为应用程序，在内核模式下运行的组件称为“软件驱动程序”  。 软件驱动程序与硬件设备不关联。 有关处理器模式的详细信息，请参阅[用户模式和内核模式](user-mode-and-kernel-mode.md)。

此图说明了与内核模式软件驱动程序通信的用户模式应用程序。

![图：显示应用程序和软件驱动程序](images/whatisadriver03.png)

## <a name="span-idadditional_notesspanspan-idadditional_notesspanspan-idadditional_notesspanadditional-notes"></a><span id="Additional_notes"></span><span id="additional_notes"></span><span id="ADDITIONAL_NOTES"></span>其他说明


软件驱动程序始终在内核模式下运行。 编写软件驱动程序的主要原因是要获取对仅在内核模式下可用的受保护数据的访问权限。 但是设备驱动程序并不总是需要访问内核模式数据和资源。 因此某些设备驱动程序在用户模式下运行。

有一类驱动程序我们还没有提到，即“总线驱动程序”  。 若要了解总线驱动程序，需要了解设备节点和设备树。 有关设备树、设备节点以及总线驱动程序的信息，请参阅[设备节点和设备堆栈](device-nodes-and-device-stacks.md)。

到目前为止，我们的说明过度简化了“函数驱动程序”的定义  。 我们说过，设备的函数驱动程序是堆栈中直接与设备通信的驱动程序。 对于直接连接到外围组件互连 (PCI) 总线的设备来说，这是正确的。 PCI 设备的函数驱动程序会获取映射到设备上的端口和内存资源的地址。 函数驱动程序通过写入这些地址直接与设备通信。 但是，在许多情况下，设备不直接连接到 PCI 总线。 而是，设备连接到连接到 PCI 总线的主机总线适配器。 例如，USB toaster 连接到主机总线适配器（称为 USB 主控制器），该适配器连接到 PCI 总线。 USB toaster 具有函数驱动程序，USB 主控制器也具有函数驱动程序。 toaster 的函数驱动程序通过向 USB 主控制器的函数驱动程序发送请求来与 toaster 间接通信。 然后，USB 主控制器的函数驱动程序与 USB 主控制器硬件直接通信，该硬件与 toaster 通信。

![图：显示 USB toaster 驱动程序和 USB 主控制器驱动程序](images/whatisadriver04.png)

 

 





