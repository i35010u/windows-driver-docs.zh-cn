---
title: 启动和 UEFI
description: 提供有关在启动过程和 UEFI 实现要求运行 Windows 10 的设备的指导。
ms.assetid: eff3f381-85fe-4bb3-a57f-3889ca8929f5
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 86b318e8d4ab86ed177faa6299a0bae263429c4d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520552"
---
# <a name="boot-and-uefi"></a>启动和 UEFI


**请注意**  本部分中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

 

运行 Windows 10 的设备具有引导到操作系统的几个要求。 设备的固件初始化所有硬件后，设备将需要确保有足够的电源来启动。 然后，需要确保如果用户想要在设备上执行更新或还原，或如果用户想要引导到主操作系统的设备，设备引导到适当的操作系统，具体取决于设备。

为了满足每种方案，Windows 10 启动过程，请使用以下组件：

-   SoC 供应商提供的固件的引导加载程序。

-   UEFI （统一可扩展固件接口） SoC 供应商提供的环境。

-   Microsoft 提供的 Windows 启动管理器。

本主题概述的启动过程中，并描述了 SoC 固件的引导加载程序，UEFI 和 Windows 启动管理器中更多详细信息。

## <a name="overview-of-the-boot-process"></a>启动过程的概述


打开 Windows 10 设备时，它将经历以下高级别过程：

1.  设备已打开，并且在运行特定于 SoC 的固件的引导加载程序，也不能初始化硬件设备上的提供紧急闪烁的功能。

2.  固件的引导加载程序启动的 UEFI 环境和手 UEFI 应用程序编写的 SoC 供应商、 Microsoft 和 Oem 的控件上。 UEFI 驱动程序和服务，可以利用这些应用程序。

3.  UEFI 环境启动 Windows 启动管理器，确定是否将启动到 FFU 闪烁或设备重置模式下，为更新 OS，或将主操作系统。

下图说明了此过程在高级别。

![适用于 windows phone 的启动过程概述](images/oem-boot-flow-overview.png)

以下是有关一些在此图中的组件的其他详细信息：

-   更新 OS 是由 Microsoft 提供的最小操作系统环境。 此 OS 专门用于安装更新。

-   FFU 闪烁模式指的闪烁到设备存储的 OS 映像的 UEFI 应用程序。 Microsoft 提供了闪烁应用程序可以在非生产方案中使用 UEFI。 Oem 还可以实现其自己 UEFI 闪烁应用程序。

## <a name="soc-firmware-boot-loaders"></a>SoC 固件的引导加载程序


SoC 固件的引导加载程序初始化硬件设备运行所需的最小集。 SoC 固件的引导加载程序设计以尽可能快速完成，而不绘制到屏幕运行时。 SoC 固件的引导加载程序完成后，设备启动到 UEFI 环境。

SoC 固件的引导加载程序还包含允许设备在启动环境不稳定，不能使用由 Microsoft 提供的闪烁工具基于 FFU 的闪烁时将刷新的紧急闪烁功能。 紧急闪烁需要特定于 SoC.的工具 有关详细信息，请与 SoC 供应商联系。

## <a name="uefi"></a>UEFI


Windows 10 利用统一可扩展固件接口 (UEFI) 以支持从 SoC 固件启动加载程序对操作系统的系统控件的切换。 UEFI 环境是在最小启动操作系统的引导设备和 Windows 10 操作系统会运行。 有关详细信息，请参阅[Windows 中的 UEFI](uefi-in-windows.md)。

## <a name="understanding-the-windows-boot-manager"></a>了解 Windows 启动管理器


Windows 启动管理器是设置了一个由 Microsoft 提供的 UEFI 应用程序*启动环境*。 在启动环境中，各个*启动应用程序*由启动管理器中启动设备启动之前为所有面向客户的方案提供的功能。

**重要**  启动环境内的所有组件都由 Microsoft 提供，不能修改、 替换，或由 Oem 省略。

 

启动应用程序可以实现以下方案的功能：

-   在启动之前设备电池充电。

-   捕获和保存脱机故障的转储 （开发人员仅生成）。

-   闪烁的具有新的映像的设备。

-   将设备重置。

-   正在更新设备。

-   启动主操作系统到设备。

下图演示了一些过程由 UEFI 环境启动之后启动管理器如下所示的关键部分。

![适用于 windows phone 的启动管理器进程](images/oem-boot-flow-detail.png)

以下步骤介绍此过程的更多详细信息：

1.  UEFI 环境启动引导管理器后，启动管理器初始化*启动库*，读取引导配置数据库，以确定哪些启动运行的应用程序和以何种顺序运行它们。 启动管理器启动启动应用程序按顺序，并完成后，每个应用程序退出返回到启动管理器。

    启动库是函数，可以扩展现有 UEFI 功能，并旨在启动环境中使用的库。 仅启动应用程序，启动引导管理器，具有访问权限的启动库。

2.  启动管理器第一次捕获由用户按下任何保留的硬件按钮组合。

3.  在非零售操作系统映像、 启动管理器接下来运行脱机崩溃转储启动应用程序允许设备以捕获从以前的操作系统会话的物理内存的快照。 时设备将重置异常上, 一个 OS 会话的内存将保留在重置。 在此情况下，脱机崩溃转储应用程序将保存该内存，并将其转换脱机故障转储文件，它可以在设备的传输和分析。 如果设备没有重置异常在以前的操作系统会话中，脱机崩溃转储应用程序将立即退出。

4.  在所有操作系统映像、 启动管理器接下来运行 mobilestartup.efi。 此应用程序运行几个启动库，其中一些仅在首次启动 （例如，预配安全启动策略） 或在有只有非零售映像 （例如，若要输入 USB 大容量存储模式下） 运行。 始终运行以下库：

    1.  首先，mobilestartup.efi 运行库，以实现 UEFI 电池充电。 此库允许用户从其设备中设备启动环境中 （或者被视为已关闭） 收费。 此库是第一次运行，以确保设备有足够的电源以完全启动。 有关涉及电池充电应用程序方案的详细信息，请参阅[启动环境中的电池充电](battery-charging-in-the-boot-environment.md)。

    2.  接下来，mobilestartup.efi 运行实现闪烁，设备重置和更新的库。 这些库确定是否在设备应启动到闪烁或设备重置模式下，或如果设备应继续更新 OS 或主操作系统。

5.  如果 mobilestartup.efi 无法启动到闪烁或设备重置模式下，启动管理器将启动与主操作系统或更新 OS。

## <a name="related-topics"></a>相关主题
[电池充电启动环境中](battery-charging-in-the-boot-environment.md)  
[UEFI 电池充电应用程序的体系结构](architecture-of-the-uefi-battery-charging-application.md)  
[Windows 中的 UEFI](uefi-in-windows.md)  



