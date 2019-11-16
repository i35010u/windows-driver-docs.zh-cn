---
title: 什么决定何时加载驱动程序
description: 什么决定何时加载驱动程序
ms.assetid: fe0f27e4-84d4-483e-8b4e-69c39ae332de
keywords:
- 筛选器驱动程序 WDK 文件系统，驱动程序加载
- 文件系统筛选器驱动程序 WDK，驱动程序加载
- 驱动程序加载 WDK 文件系统
- 正在加载驱动程序 WDK 文件系统
- 驱动程序启动类型 WDK 文件系统
- 启动类型 WDK 文件系统
- 加载顺序组 WDK 文件系统
- SERVICE_BOOT_START
- SERVICE_SYSTEM_START
- SERVICE_AUTO_START
- SERVICE_DEMAND_START
- SERVICE_DISABLED
- 启动驱动程序 WDK 文件系统
- 启动驱动程序 WDK 文件系统
ms.date: 10/16/2019
ms.localizationpriority: medium
ms.openlocfilehash: eaab9ad4ffc1ecd107dade126a9fa3b13152fee6
ms.sourcegitcommit: 2a1c24db881ed843498001493c3ce202c9aa03f1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/16/2019
ms.locfileid: "74128466"
---
# <a name="what-determines-when-a-driver-is-loaded"></a>什么决定何时加载驱动程序

> [!NOTE]
> 为了获得最佳的可靠性和性能，请使用[文件系统筛选器驱动程序](filter-manager-and-minifilter-driver-architecture.md)，而不是旧的文件系统筛选器驱动程序 若要将旧驱动程序移植到微筛选器驱动程序，请参阅[迁移旧筛选器驱动程序的准则](guidelines-for-porting-legacy-filter-drivers.md)。

在浏览系统启动顺序中的文件系统驱动程序的加载时间和方式之前，必须了解驱动程序启动类型和加载顺序组。

## <a name="driver-start-types"></a>驱动程序启动类型

内核模式驱动程序的*启动类型*指定是在系统启动期间还是之后加载驱动程序。 有五种可能的启动类型：

- SERVICE_BOOT_START （0x00000000）  
  指示由操作系统（OS）加载程序启动的驱动程序。 文件系统筛选器驱动程序通常使用此开始类型或 SERVICE_DEMAND_START。 在 Microsoft Windows XP 和更高版本的系统上，筛选器必须使用此启动类型才能利用新的[文件系统筛选器加载顺序组](load-order-groups-for-file-system-filter-drivers.md)。

- SERVICE_SYSTEM_START （0x00000001）  
  指示在 OS 初始化期间启动了驱动程序。 此启动类型由文件系统识别器使用。 除了下面列出的 "SERVICE_DISABLED" 文件系统（包括网络文件系统组件）以外的文件系统，通常使用此开始类型或 SERVICE_DEMAND_START。 此启动类型还由设备驱动程序使用，用于在系统初始化期间枚举的 PnP 设备，但不需要加载系统。

- SERVICE_AUTO_START （0x00000002）  
  指示在系统启动期间由服务控制管理器启动的驱动程序。 很少使用。

- SERVICE_DEMAND_START （0x00000003）  
  指示由 PnP 管理器（对于设备驱动程序）或服务控制管理器（对于文件系统和文件系统筛选器驱动程序），按需启动驱动程序。

- SERVICE_DISABLED （0x00000004）  
  指示 OS 加载程序、服务控制管理器或 PnP 管理器未启动的驱动程序。 由文件系统识别器（它们是启动文件系统时除外）或其他文件系统（EFS）加载的文件系统使用。 此类文件系统包括 CDFS、EFS、FastFat、NTFS 和 UDF。 还用于在调试过程中临时禁用驱动程序。

## <a name="specifying-start-type"></a>指定开始类型

驱动程序编写器可以通过以下任一方式在安装时指定驱动程序的启动类型：

- 通过在驱动程序的 INF 文件中，在[**AddService**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addservice-directive)指令所引用的*服务安装部分*中为**StartType**条目指定所需的启动类型。 此方法在 ServiceInstall 部分中进行了介绍。

- 通过用户模式安装程序调用**CreateService**或**ChangeServiceConfig**时，为*dwStartType*参数传递所需的启动类型。 Microsoft Windows SDK 文档中的**CreateService**和**ChangeServiceConfig**的参考条目中介绍了此方法。

## <a name="driver-load-order-groups"></a>驱动程序加载顺序组

在 SERVICE_BOOT_START 和 SERVICE_SYSTEM_START 启动类型中，每个驱动程序的*加载顺序组*都指定了加载驱动程序的相对顺序。

启动类型为 SERVICE_BOOT_START 的驱动程序称为*启动（或启动）驱动程序*。 在 Microsoft Windows 2000 及更早版本的系统上，许多启动驱动程序的筛选器属于 "筛选器" 组。 在 Microsoft Windows XP 和更高版本的系统上，作为启动驱动程序的筛选器通常属于一个新的 FSFilter 加载顺序组。 [文件系统筛选器驱动程序的加载顺序组](load-order-groups-for-file-system-filter-drivers.md)中详细介绍了这些加载顺序组。

其启动类型为 SERVICE_SYSTEM_START 的驱动程序也按其所属的加载顺序组的顺序进行加载。 但是，在加载所有启动驱动程序之前，不会加载任何系统启动驱动程序。

> [!NOTE]
> 对于其启动类型为 SERVICE_AUTO_START、SERVICE_DEMAND_START 或 SERVICE_DISABLED 的驱动程序，将忽略加载顺序组。

可在**HKEY_LOCAL_MACHINE \system\currentcontrolset\control**注册表项的**ServiceGroupOrder**子项下找到完整的、有序的加载顺序组列表。

相同的负载组排序用于 SERVICE_BOOT_START 和 SERVICE_SYSTEM_START 驱动程序。 但是，在加载任何 SERVICE_SYSTEM_START 驱动程序之前，将加载并启动所有 SERVICE_BOOT_START 驱动程序。

## <a name="specifying-load-order-group"></a>指定加载顺序组

在安装时，驱动程序编写器可以通过以下任一方式来指定驱动程序的加载顺序组：

- 通过在驱动程序的 INF 文件中，为**AddService**指令所引用的*服务安装部分*中的**LoadOrderGroup**条目指定所需的加载顺序组。 此方法在 ServiceInstall 部分中进行了介绍。

- 通过用户模式安装程序调用**CreateService**或**ChangeServiceConfig**时，为*lpLoadOrderGroup*参数传递所需的启动类型。 Microsoft Windows SDK 文档中的**CreateService**和**ChangeServiceConfig**的参考条目中介绍了此方法。

有关驱动程序加载顺序和加载顺序组的更多常规信息，请参阅[指定驱动程序加载顺序](https://docs.microsoft.com/windows-hardware/drivers/install/specifying-driver-load-order)。
