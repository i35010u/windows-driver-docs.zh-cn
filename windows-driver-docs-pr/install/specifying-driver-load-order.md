---
title: 指定驱动程序加载顺序
description: 指定驱动程序加载顺序
ms.assetid: 2e06671a-5664-4042-bc7a-e8ab12938cea
keywords:
- INF 文件 WDK 设备安装，驱动程序加载顺序
- 驱动程序加载顺序 WDK INF 文件
- 加载顺序 WDK INF 文件
- 服务安装部分 WDK INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 11f055ce9426c61d3baf30752039dec44fe95a58
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541072"
---
# <a name="specifying-driver-load-order"></a>指定驱动程序加载顺序





适用于大多数设备的计算机上的设备的物理层次结构确定 Windows 和 PnP 管理器加载驱动程序的顺序。 Windows 和 PnP 管理器配置系统根设备后，启动的设备，然后他们配置根设备 （例如，是 PCI 适配器），这些设备的子级的子设备和其他操作。 PnP 管理器加载每个设备的驱动程序设备是经过配置之后，如果驱动程序以前未加载的另一台设备。

INF 文件中的设置可以影响驱动程序加载顺序。 本主题介绍相关供应商应该在中指定的值*服务安装部分*由驱动程序的引用[ **INF AddService 指令**](inf-addservice-directive.md)。 具体而言，本主题讨论**StartType**， **BootFlags**， **LoadOrderGroup**，以及**依赖项**条目。

驱动程序应遵循这些规则用于指定**StartType**:

-   即插即用驱动程序

    即插即用驱动程序应具有指定的 PnP 管理器可以加载驱动程序时即插即用管理器查找设备驱动程序服务的 SERVICE_DEMAND_START (0x3) 启动类型。

-   启动计算机所需设备驱动程序

    如果设备需要来启动计算机，这些设备驱动程序应具有 SERVICE_BOOT_START (0x0) 的启动类型。

-   非*引导启动驱动程序*，用于检测设备不是可 PnP 枚举

    对于不是可 PnP 枚举设备，驱动程序报告设备的即插即用的管理器为通过调用[ **IoReportDetectedDevice**](https://msdn.microsoft.com/library/windows/hardware/ff549597)。 这样的驱动程序应具有的启动类型 SERVICE_SYSTEM_START (0x01)，因此 Windows 将在系统初始化期间加载的驱动程序。

    驱动程序该报告非 PnP 硬件应设置此启动类型。 如果驱动程序服务 （即插即用和非 PnP 设备），它应设置此启动类型。

-   必须由服务控制管理器启动非 PnP 驱动程序

    此类驱动程序应具有的启动类型 SERVICE_AUTO_START (0x02)。 即插即用驱动程序不设置此启动类型。

应编写的即插即用驱动程序，以便 Windows 会在配置设备时加载的驱动程序服务。 相反，驱动程序应该能够将卸载即插即用管理器确定，不再有任何时间设备提供的驱动程序服务。 即插即用驱动程序应依赖于唯一驱动程序加载顺序如下所示：

1.  子设备的驱动程序可以依赖于父设备的驱动程序加载了这一事实。

2.  设备堆栈中的驱动程序可以依赖于它下面的任何驱动程序已加载的这一事实。

    例如，功能驱动程序可以是某些加载任何更低的筛选器驱动程序。

    但是，请注意设备堆栈中的驱动程序不能依赖于设备的低级驱动程序后按顺序加载，因为该驱动程序可能先前加载配置另一台设备时。

筛选器组中的筛选器驱动程序不能预测及其负载排序。 例如，如果设备具有三个已注册的上限筛选器驱动程序，这些三个的驱动程序都将加载功能驱动程序后，但可能是其上限筛选器组中的任何顺序加载。

如果驱动程序包含在另一个驱动程序的显式加载顺序依赖关系，该依赖项应实现通过父/子关系。 子设备的驱动程序可以依赖于父设备之前加载子驱动程序加载的驱动程序。

为了强调设置正确的重要性**StartType**值，以下列表说明了如何使用 Windows 和 PnP 管理器**StartType** INF 文件中的条目：

1.  在系统启动时，操作系统加载程序加载驱动程序的类型 SERVICE_BOOT_START 之前它将控制转移到内核。 当内核获取控件时，这些驱动程序是在内存中。

    引导启动驱动程序可以使用 INF **LoadOrderGroup**条目进行排序其加载。 （引导启动驱动程序之前加载配置大多数设备，使其加载顺序不能由设备层次结构。）操作系统会忽略 INF**依赖项**引导启动驱动程序的条目。

2.  PnP 管理器调用**DriverEntry**例程 SERVICE_BOOT_START 驱动程序以便将驱动程序可以提供服务的启动设备。

    如果启动设备具有子设备，将枚举这些设备。 子设备配置的如果其驱动程序也是引导启动驱动程序的启动。 如果设备的驱动程序不是所有引导启动驱动程序，即插即用管理器创建的设备节点 (*devnode*) 设备，但不会启动设备。

3.  所有启动驱动程序已都加载并启动设备启动后，即插即用管理器配置的即插即用设备的其余部分，并加载其驱动程序。

    PnP 管理器将沿着尚未开始设备树 (即，从上一步任何 nonstarted 的 devnodes)。 每个设备启动时，即插即用管理器枚举的子级的设备，如果有的话。

    PnP 管理器配置这些设备，如加载的设备驱动程序*而不考虑*的驱动程序的**StartType**值 (例外**StartType**是服已禁用） 然后才能继续启动设备。 许多这些驱动程序是 SERVICE_DEMAND_START 驱动程序。

    PnP 管理器将忽略由于 INF 而创建的注册表条目**依赖项**条目并**LoadOrderGroup**驱动程序，它在此步骤中将加载项。 负载排序根据物理设备层次结构。

    在此步骤结束时，所有这些设备配置，不可 PnP 枚举以及后代的那些设备的设备除外。 (后代可能或可能不是可 PnP 枚举。)

4.  PnP 管理器加载的驱动程序**StartType** SERVICE_SYSTEM_START 尚未加载。

    这些驱动程序检测并报告其非 PnP 设备。 PnP 管理器将处理结果的 INF 的注册表项**LoadOrderGroup**这些驱动程序的条目。 它会忽略由于 INF 而创建的注册表项**依赖项**这些驱动程序的条目。

5.  服务控制管理器加载的驱动程序**StartType** SERVICE_AUTO_START 尚未加载。

    服务控制管理器处理相对于服务的服务数据库信息**DependOnGroup**并**DependOnServices**。 此信息是从**依赖项**INF 中的条目**AddService**条目。 请注意，**依赖项**因为任何必需的即插即用驱动程序已加载到系统启动的前面步骤中，信息只处理的非 PnP 驱动程序。 服务控制管理器将忽略 INF **LoadOrderGroup**信息。

    请参阅有关服务控制管理器的详细信息的 Microsoft Windows SDK 文档。

### <a name="using-bootflags-to-promote-a-drivers-starttype-at-boot-depending-on-boot-scenario"></a>使用 BootFlags 将提升在具体取决于引导方案的启动驱动程序的启动类型

操作系统可以升级的驱动程序**StartType**成为具体取决于启动开始驱动**BootFlags**驱动程序的 INF 中指定的值。 你可以指定一个或多个 （或运算） 的以下数字值表示为十六进制值的 INF 文件中：

-   如果驱动程序应将其升级为在网络启动的引导启动驱动程序，指定**0x1** (CM_SERVICE_NETWORK_BOOT_LOAD)。
-   如果应在从 VHD 启动升级驱动程序，指定**0x2** (CM_SERVICE_VIRTUAL_DISK_BOOT_LOAD)
-   如果驱动程序应将其升级从 USB 磁盘启动时，指定**0x4** (CM_SERVICE_USB_DISK_BOOT_LOAD)。
-   如果驱动程序应将其升级从 SD 存储启动时，指定**0x8** (CM_SERVICE_SD_DISK_BOOT_LOAD)
-   如果驱动程序应将其升级从磁盘上的 USB 3.0 控制器启动时，指定**0x10** (CM_SERVICE_USB3_DISK_BOOT_LOAD)。
-   如果驱动程序应将其升级时引导测量启用启动，则指定**0x20** (CM_SERVICE_MEASURED_BOOT_LOAD)。
-   如果驱动程序应将其升级时引导启用验证程序启动，则指定**0x40** (CM_SERVICE_VERIFIER_BOOT_LOAD)。
-   如果应在 WinPE 启动升级驱动程序，指定**0x80** (CM_SERVICE_WINPE_BOOT_LOAD)。

有关升级驱动程序的详细信息**StartType**在启动，具体取决于启动方案中，请参阅[ **INF AddService 指令**](inf-addservice-directive.md)。

 

 





