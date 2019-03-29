---
title: 什么决定何时加载驱动程序
description: 什么决定何时加载驱动程序
ms.assetid: fe0f27e4-84d4-483e-8b4e-69c39ae332de
keywords:
- 筛选器驱动程序 WDK 文件系统，加载的驱动程序
- 文件系统筛选器驱动程序 WDK，加载的驱动程序
- 正在加载 WDK 文件系统驱动程序
- 加载驱动程序 WDK 文件系统
- 驱动程序开始类型 WDK 文件系统
- 启动类型 WDK 文件系统
- 加载顺序组 WDK 文件系统
- SERVICE_BOOT_START
- SERVICE_SYSTEM_START
- SERVICE_AUTO_START
- SERVICE_DEMAND_START
- SERVICE_DISABLED
- 启动驱动程序 WDK 文件系统
- 引导启动驱动程序 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48beeb607b42424f5c7337512532b499a23585ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562152"
---
# <a name="what-determines-when-a-driver-is-loaded"></a>什么决定何时加载驱动程序


## <span id="ddk_what_determines_when_a_driver_is_loaded_if"></span><span id="DDK_WHAT_DETERMINES_WHEN_A_DRIVER_IS_LOADED_IF"></span>


浏览之前何时以及如何在系统启动过程中，加载文件系统驱动程序就需要了解驱动程序启动类型和组的加载顺序。

### <a name="span-idddkdriverstarttypesifspanspan-idddkdriverstarttypesifspandriver-start-types"></a><span id="ddk_driver_start_types_if"></span><span id="DDK_DRIVER_START_TYPES_IF"></span>驱动程序启动类型

内核模式驱动程序*启动类型*指定是否要加载期间或之后系统启动驱动程序。 有五种可能的启动类型：

<span id="SERVICE_BOOT_START__0x00000000_"></span><span id="service_boot_start__0x00000000_"></span><span id="SERVICE_BOOT_START__0X00000000_"></span>服务\_启动\_开始 (0x00000000)  
指示由操作系统 (OS) 加载程序启动的驱动程序。 文件系统筛选器驱动程序通常使用此启动类型或服务\_需\_开始。 在 Microsoft Windows XP 和更高版本的系统，筛选器必须使用此启动类型才能充分利用新[文件系统筛选器加载顺序组](load-order-groups-for-file-system-filter-drivers.md)。

<span id="SERVICE_SYSTEM_START__0x00000001_"></span><span id="service_system_start__0x00000001_"></span><span id="SERVICE_SYSTEM_START__0X00000001_"></span>服务\_系统\_开始 (0x00000001)  
指示操作系统初始化过程中启动了驱动程序。 此启动类型可供文件系统识别器。 除了下下面列出的文件系统"服务\_禁用，"文件系统 （包括网络文件系统组件） 通常使用此启动类型或服务\_需\_开始。 此启动类型还用于设备驱动程序通过枚举在系统初始化过程但不是需要加载系统的即插即用设备。

<span id="SERVICE_AUTO_START__0x00000002_"></span><span id="service_auto_start__0x00000002_"></span><span id="SERVICE_AUTO_START__0X00000002_"></span>服务\_自动\_开始 (0x00000002)  
指示在系统启动期间启动服务控制管理器的驱动程序。 很少使用。

<span id="SERVICE_DEMAND_START__0x00000003_"></span><span id="service_demand_start__0x00000003_"></span><span id="SERVICE_DEMAND_START__0X00000003_"></span>服务\_需\_开始 (0x00000003)  
指示启动按需、 即插即用管理器 （适用于设备驱动程序） 或由服务控制管理器 （适用于文件系统和文件系统筛选器驱动程序） 的驱动程序。

<span id="SERVICE_DISABLED__0x00000004_"></span><span id="service_disabled__0x00000004_"></span><span id="SERVICE_DISABLED__0X00000004_"></span>服务\_已禁用 (0x00000004)  
指示由操作系统加载程序，即插即用管理器或服务控制管理器，未启动的驱动程序。 使用的文件系统加载的文件系统识别程序 （除非它们启动文件系统） 或 （对于 EFS) 被另一个文件系统。 此类文件系统包含 CDFS、 EFS、 FastFat、 NTFS 和 UDF。 此外用于在调试期间暂时禁用驱动程序。

### <a name="span-idddkspecifyingstarttypeifspanspan-idddkspecifyingstarttypeifspanspecifying-start-type"></a><span id="ddk_specifying_start_type_if"></span><span id="DDK_SPECIFYING_START_TYPE_IF"></span>指定的启动类型

驱动程序编写器可以指定在安装时，在以下两种方式中的驱动程序的启动类型：

-   通过指定的所需的启动类型**StartType**中的条目*服务安装部分*引用[ **AddService** ](https://msdn.microsoft.com/library/windows/hardware/ff546326)驱动程序的 INF 文件中的指令。 ServiceInstall 部分中介绍了这些方法。

-   通过传递所需启动类型为*dwStartType*参数调用时**CreateService**或**执行 ChangeServiceConfig**从用户模式下安装程序。 此方法所述的引用项**CreateService**并**执行 ChangeServiceConfig** Microsoft Windows SDK 文档中。

### <a name="span-idddkdriverloadordergroupsifspanspan-idddkdriverloadordergroupsifspandriver-load-order-groups"></a><span id="ddk_driver_load_order_groups_if"></span><span id="DDK_DRIVER_LOAD_ORDER_GROUPS_IF"></span>驱动程序加载顺序组

在服务中\_引导\_开始和服务\_系统\_START 启动类型，在其中加载驱动程序的相对顺序指定的每个驱动程序*加载顺序组*。

驱动程序的启动类型是服务\_引导\_称为开始*启动 （或引导启动） 驱动程序*。 在 Microsoft Windows 2000 和更早的系统，会启动驱动程序的大多数筛选器都属于"筛选器"组。 在 Microsoft Windows XP 和更高版本的系统的筛选器会启动驱动程序通常属于新 FSFilter 之一加载顺序组。 中详细介绍了这些加载顺序组[文件系统筛选器驱动程序的加载顺序组](load-order-groups-for-file-system-filter-drivers.md)。

驱动程序的启动类型是服务\_系统\_开始也会加载按照加载顺序组到其所属的顺序。 但是，任何系统启动驱动程序不加载之前后已加载所有启动驱动程序。

**请注意**  加载顺序组对于其启动类型是服务的驱动程序将忽略\_自动\_开始，服务\_需\_开始或服务\_已禁用。

 

可以下找到完整的有序的加载顺序组列表**ServiceGroupOrder**以下注册表项的子项：

**HKEY\_LOCAL\_MACHINE\\System\\CurrentControlSet\\Control**

相同的负载组顺序用于 SERVICE\_引导\_开始和服务\_系统\_启动的驱动程序。 但是，在所有 SERVICE\_引导\_启动的驱动程序加载和任何服务之前启动\_系统\_加载启动的驱动程序。

### <a name="span-idddkspecifyingloadordergroupifspanspan-idddkspecifyingloadordergroupifspanspecifying-load-order-group"></a><span id="ddk_specifying_load_order_group_if"></span><span id="DDK_SPECIFYING_LOAD_ORDER_GROUP_IF"></span>指定加载顺序组

驱动程序编写器可以指定在安装时，在以下两种方式中的驱动程序的加载顺序组：

-   通过指定的所需的加载顺序组**LoadOrderGroup**中的条目*服务安装部分*引用**AddService**指令中的驱动程序 INF文件。 ServiceInstall 部分中介绍了这些方法。

-   通过传递所需启动类型为*lpLoadOrderGroup*参数调用时**CreateService**或**执行 ChangeServiceConfig**从用户模式下安装程序。 此方法所述的引用项**CreateService**并**执行 ChangeServiceConfig** Microsoft Windows SDK 文档中。

有关驱动程序的更多常规信息加载顺序并加载顺序组，请参阅[指定驱动程序加载顺序](https://msdn.microsoft.com/library/windows/hardware/ff552319)。

 

 




