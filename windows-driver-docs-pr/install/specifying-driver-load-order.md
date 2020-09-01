---
title: 指定驱动程序加载顺序
description: 指定驱动程序加载顺序
ms.assetid: 2e06671a-5664-4042-bc7a-e8ab12938cea
keywords:
- INF 文件 WDK 设备安装，驱动程序加载顺序
- 驱动程序加载 WDK INF 文件
- 负载顺序 WDK INF 文件
- 服务-安装 WDK INF 文件部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c2ae56399f1976b5cbac18ec12110bb0fb756c3
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097053"
---
# <a name="specifying-driver-load-order"></a>指定驱动程序加载顺序





对于大多数设备，计算机上设备的物理层次结构决定了 Windows 和 PnP 管理器加载驱动程序的顺序。 Windows 和 PnP 管理器配置从系统根设备开始的设备，然后配置根设备的子设备 (例如，PCI 适配器) 、这些设备的子级等等。 如果先前未为其他设备加载驱动程序，PnP 管理器会在配置设备时加载每个设备的驱动程序。

INF 文件中的设置可能会影响驱动程序的加载顺序。 本主题介绍供应商在驱动程序的[**INF AddService 指令**](inf-addservice-directive.md)引用的*服务安装部分*中应指定的相关值。 具体而言，本主题讨论 **StartType**、 **BootFlags**、 **LoadOrderGroup**和 **依赖** 项条目。

驱动程序应遵循以下规则来指定 **StartType**：

-   PnP 驱动程序

    PnP 驱动程序的启动类型应为 SERVICE_DEMAND_START (0x3) ，指定 PnP 管理器找到驱动程序服务的设备时，PnP 管理器可以加载驱动程序。

-   启动计算机所需的设备驱动程序

    如果设备需要启动计算机，则设备的驱动程序的启动类型应为 SERVICE_BOOT_START (0x0) 。

-   检测非 PnP) 设备 (的非*启动启动驱动程序*

    对于非 PnP 可枚举设备，驱动程序通过调用 [**IoReportDetectedDevice**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioreportdetecteddevice)向 pnp 管理器报告设备。 此类驱动程序的启动类型应 SERVICE_SYSTEM_START (0x01) 因此 Windows 将在系统初始化过程中加载驱动程序。

    只有报表非 PnP 硬件的驱动程序应设置此启动类型。 如果驱动程序同时服务 PnP 和非 PnP 设备，则应设置此启动类型。

-   必须由服务控制管理器启动的非 PnP 驱动程序

    此类驱动程序的启动类型应 SERVICE_AUTO_START)  (0x02。 PnP 驱动程序不得设置此启动类型。

应该写入 PnP 驱动程序，以便可以在 Windows 配置驱动程序服务的设备时加载该驱动程序。 相反，只要 PnP 管理器确定不存在驱动程序服务的设备，就应该能够卸载该驱动程序。 PnP 驱动程序应依赖的唯一驱动程序加载排序如下所示：

1.  子设备的驱动程序可能取决于父设备的驱动程序的加载情况。

2.  设备堆栈中的驱动程序可能取决于其下的所有驱动程序都已加载。

    例如，函数驱动程序可以确定是否加载了任何较低筛选器驱动程序。

    但请注意，设备堆栈中的驱动程序不能依赖于在设备的较低驱动器上按顺序加载，因为在配置另一台设备时可能会加载该驱动程序。

筛选器组中的筛选器驱动程序无法预测其负载排序。 例如，如果设备有三个已注册的高级筛选器驱动程序，这三个驱动程序将在函数驱动程序之后加载，但可以在其上限组内按任意顺序加载。

如果驱动程序在另一个驱动程序上具有显式的加载顺序依赖关系，则应通过父/子关系实现该依赖项。 子设备的驱动程序可能依赖于加载子驱动程序之前加载的父设备的驱动程序。

为了强调设置正确的 **StartType** 值的重要性，下表介绍了 Windows 和 PnP 管理器如何在 INF 文件中使用 **StartType** 条目：

1.  在系统启动时，操作系统加载程序会加载类型 SERVICE_BOOT_START 的驱动程序，然后再将控制权移交给内核。 当内核获得控制时，这些驱动程序将在内存中。

    启动驱动程序可以使用 INF **LoadOrderGroup** 项对其加载进行排序。 在配置大多数设备之前，将加载 (启动启动驱动程序，因此无法通过设备层次结构确定其加载顺序。 ) 操作系统会忽略引导启动驱动程序的 INF **依赖** 项条目。

2.  PnP 管理器调用 SERVICE_BOOT_START 驱动程序的 **DriverEntry** 例程，以便驱动程序可以为启动设备服务。

    如果启动设备具有子设备，则会枚举这些设备。 如果子设备的驱动程序也是启动启动驱动程序，则会配置并启动它们。 如果设备的驱动程序并非所有启动启动驱动程序，则 PnP 管理器会为设备创建一个设备节点 (*devnode*) ，但不会启动该设备。

3.  在所有启动驱动程序都已加载并启动启动设备后，PnP 管理器将配置 PnP 设备的其余部分并加载其驱动程序。

    PnP 管理器会执行尚未启动的设备树， (即上一步骤) 中的任何 nonstarted devnodes。 每个设备启动时，PnP 管理器会枚举设备的子节点（如果有）。

    当它配置这些**设备时，** PnP 管理器加载设备的驱动程序，*而不考虑*驱动程序的**StartType**值 (除非在继续启动设备之前 SERVICE_DISABLED) 。 其中许多驱动程序都是 SERVICE_DEMAND_START 驱动程序。

    PnP 管理器会忽略作为 INF **依赖** 项的结果创建的注册表项，以及在此步骤中加载的驱动程序的 **LoadOrderGroup** 项。 负载顺序基于物理设备层次结构。

    在此步骤结束时，将配置所有设备，但不是可自行枚举的设备以及这些设备的后代。  (子代可能会也可能不是可 ) 。

4.  PnP 管理器加载尚未加载的 **StartType** SERVICE_SYSTEM_START 的驱动程序。

    这些驱动程序检测并报告其非 PnP 设备。 PnP 管理器处理这些驱动程序的 INF **LoadOrderGroup** 条目结果的注册表项。 它将忽略由于这些驱动程序的 INF **依赖** 项而创建的注册表项。

5.  服务控制管理器加载尚未加载的 **StartType** SERVICE_AUTO_START 的驱动程序。

    服务控制管理器根据服务的 " **DependOnGroup** " 和 " **DependOnServices**" 处理服务数据库信息。 此信息来自 INF **AddService**条目中的**依赖**项条目。 请注意，仅为非 PnP 驱动程序处理 **依赖关系** 信息，因为在以前的系统启动步骤中加载了任何必需的 pnp 驱动程序。 服务控制管理器忽略 INF **LoadOrderGroup** 信息。

    有关服务控制管理器的详细信息，请参阅 Microsoft Windows SDK 文档。

### <a name="using-bootflags-to-promote-a-drivers-starttype-at-boot-depending-on-boot-scenario"></a>使用 BootFlags 在启动时根据启动方案升级驱动程序的 StartType

操作系统可以根据驱动程序 INF 中指定的**BootFlags**值将驱动程序的**StartType**提升为启动启动驱动程序。 可以在 INF 文件中指定以下数值的一个或多个 (运算) ，以十六进制值表示：

-   如果驱动程序应升级为网络启动时的启动启动驱动程序，请指定 **0x1** (CM_SERVICE_NETWORK_BOOT_LOAD) 。
-   如果在从 VHD 启动时应升级驱动程序，请指定 **0x2** (CM_SERVICE_VIRTUAL_DISK_BOOT_LOAD) 
-   如果从 USB 磁盘启动时应升级驱动程序，请指定 **0x4** (CM_SERVICE_USB_DISK_BOOT_LOAD) 。
-   如果从 SD 存储启动时应升级驱动程序，请指定 **0x8** (CM_SERVICE_SD_DISK_BOOT_LOAD) 
-   如果从 USB 3.0 控制器上的磁盘启动时应升级驱动程序，请指定 **0x10** (CM_SERVICE_USB3_DISK_BOOT_LOAD) 。
-   如果在启用了度量启动的情况下启动时应升级驱动程序，请指定 **0x20** (CM_SERVICE_MEASURED_BOOT_LOAD) 。
-   如果在启用了验证程序启动时升级驱动程序，请指定 **0x40** (CM_SERVICE_VERIFIER_BOOT_LOAD) 。
-   如果在 WinPE 启动时应升级驱动程序，请指定 **0x80** (CM_SERVICE_WINPE_BOOT_LOAD) 。

有关在启动时升级驱动程序的 **StartType** 的详细信息，请参阅 [**INF AddService 指令**](inf-addservice-directive.md)。

 

