---
title: 启动和 UEFI
description: 提供有关运行 Windows 10 的设备的启动过程和 UEFI 实现要求的指导。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b143a841d73405e9f7792333c6b9c0f7564bb122
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789137"
---
# <a name="boot-and-uefi"></a>启动和 UEFI


**注意**  本节中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

 

运行 Windows 10 的设备有多个用于启动操作系统的要求。 设备固件初始化所有硬件后，设备需要确保有足够的功率来启动。 然后，设备需要确保设备启动到相应的操作系统中，具体取决于用户是否要在设备上执行更新或还原，或用户是否想要将设备启动到主操作系统。

为了适应每个方案，Windows 10 boot 进程使用以下组件：

-   SoC 供应商提供的固件启动加载程序。

-   统一可扩展固件接口 SoC 供应商提供的) 环境的 UEFI (。

-   Microsoft 提供的 Windows 启动管理器。

本主题概述了启动过程，并更详细地介绍了 SoC 固件启动加载程序、UEFI 和 Windows 启动管理器。

## <a name="overview-of-the-boot-process"></a>启动过程概述


当 Windows 10 设备处于开启状态时，它会经历以下高级过程：

1.  设备已打开并运行 SoC 特定的固件启动加载程序，它们可初始化设备上的硬件并提供紧急闪烁功能。

2.  固件启动加载程序启动 UEFI 环境，并将控制权移交给 SoC 供应商、Microsoft 和 Oem 编写的 UEFI 应用程序。 这些应用程序可以利用 UEFI 驱动程序和服务。

3.  UEFI 环境启动 Windows 启动管理器，该管理器确定是启动到 FFU 闪烁还是设备重置模式、更新操作系统或主操作系统。

下图演示了此过程的较高级别。

![windows phone 的启动过程概述](images/oem-boot-flow-overview.png)

下面是有关此关系图中某些组件的其他详细信息：

-   更新操作系统是 Microsoft 提供的最低操作系统环境。 此 OS 专门用于安装更新。

-   FFU 闪烁模式是指将 OS 映像闪烁到设备存储的 UEFI 应用程序。 Microsoft 提供了可在非生产方案中使用的 UEFI 闪烁的应用程序。 Oem 还可以实现自己的 UEFI 闪烁应用程序。

## <a name="soc-firmware-boot-loaders"></a>SoC 固件启动加载加载


SoC 固件启动加载程序将初始化设备运行所需的最小硬件集。 SoC 固件启动加载加载设计为尽可能快地完成，在运行时不会在屏幕上绘制任何内容。 SoC 固件启动加载加载机完成后，设备将启动到 UEFI 环境中。

SoC 固件启动加载程序还包含一项紧急闪烁功能，该功能允许在启动环境不稳定时刷新设备，并且无法使用 Microsoft 提供的闪烁工具进行 FFU 的闪烁。 紧急闪烁需要特定于 SoC 的工具。 有关详细信息，请联系 SoC 供应商。

## <a name="uefi"></a>UEFI


Windows 10 统一可扩展固件接口 (UEFI) ，以支持从 SoC 固件启动加载程序到操作系统的系统控制。 UEFI 环境是在其上启动设备和运行 Windows 10 操作系统的最小启动操作系统。 有关详细信息，请参阅 [Windows 中的 UEFI](uefi-in-windows.md)。

## <a name="understanding-the-windows-boot-manager"></a>了解 Windows 启动管理器


Windows 启动管理器是 Microsoft 提供的一个 UEFI 应用程序，用于设置 *启动环境*。 在引导环境内，启动管理器启动的单个 *启动应用程序* 在设备启动之前为所有面向客户的方案提供了功能。

**重要提示**  启动环境中的所有组件都由 Microsoft 提供，不能修改、替换或被 Oem 忽略。

 

启动应用程序在以下情况下实现功能：

-   在启动前对设备电池充电。

-   捕获并保存脱机故障转储 (仅) 开发人员构建。

-   使用新映像闪烁设备。

-   正在重置设备。

-   更新设备。

-   将设备启动到主操作系统。

下图说明了启动管理器在 UEFI 环境启动后遵循的部分重要部分。

![适用于 windows phone 的启动管理器进程](images/oem-boot-flow-detail.png)

以下步骤更详细地介绍了此过程：

1.  在 UEFI 环境启动启动管理器后，启动管理器将初始化 *启动库*，读取启动配置数据库，以确定要运行的启动应用程序以及运行这些程序的顺序。 启动管理器按顺序启动启动应用程序，并在完成后，每个应用程序都将退出启动管理器。

    启动库是扩展现有 UEFI 功能的函数库，设计用于引导环境中。 只有启动管理器启动的启动应用程序才能访问启动库。

2.  启动管理器首先捕获用户按下的所有保留硬件按钮组合。

3.  在非零售 OS 映像中，启动管理器接下来运行脱机故障转储引导应用程序，该应用程序允许设备捕获先前 OS 会话中物理内存的快照。 当设备异常重置时，将在重置期间保留以前的 OS 会话的内存。 发生这种情况时，脱机崩溃转储应用程序将保存该内存并将其转换为脱机故障转储文件，该文件可以从设备传输并进行分析。 如果设备在以前的 OS 会话中未异常重置，则脱机故障转储应用程序将立即退出。

4.  在所有 OS 映像中，启动管理器接下来运行 mobilestartup。 此应用程序运行多个启动库，其中某些启动库仅在首次启动时运行 (例如，设置安全启动策略) 或仅在非零售映像中 (例如，要输入 USB 大容量存储模式) 。 始终运行以下库：

    1.  首先，mobilestartup 运行实现 UEFI 电池充电的库。 此库允许用户在设备处于引导环境中时对其设备进行计费， (或被视为已关闭) 。 此库首先运行，以确保设备有足够的电量来完全启动。 有关涉及电池充电应用程序的方案的详细信息，请参阅 [启动环境中的电池充电](battery-charging-in-the-boot-environment.md)。

    2.  接下来，mobilestartup 运行实现闪烁、设备重置和更新的库。 这些库确定设备应启动到闪烁还是设备重置模式，或者设备是否应继续到更新操作系统或主操作系统。

5.  如果 mobilestartup 未启动到闪烁或设备重置模式，则启动管理器将启动到主操作系统或更新操作系统。

## <a name="related-topics"></a>相关主题
[启动环境中的电池充电](battery-charging-in-the-boot-environment.md)  
[UEFI 电池充电应用程序的体系结构](architecture-of-the-uefi-battery-charging-application.md)  
[Windows 中的 UEFI](uefi-in-windows.md)  



