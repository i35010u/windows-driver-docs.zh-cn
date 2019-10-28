---
title: 硬件资源
description: 硬件资源
ms.assetid: c7a6997b-34f9-4dd9-b384-2321a8b5ce54
keywords:
- 资源描述符 WDK PnP
- PnP WDK 内核，硬件资源
- 即插即用 WDK 内核，硬件资源
- 资源要求列出了 WDK PnP
- 资源列表 WDK PnP
- 已分配资源 WDK PnP
- 要求列出了 WDK PnP
- 注册表 WDK PnP
- 逻辑配置 WDK PnP
- 启动配置 WDK PnP
- 强制配置 WDK PnP
- 筛选的配置 WDK PnP
- 替代配置 WDK PnP
- 配置类型 WDK PnP
- 分配的配置 WDK PnP
- 基本配置 WDK PnP
- 硬件资源
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e22ef29044d442186f668ed1dfc88ec4a7cf6a1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838646"
---
# <a name="hardware-resources"></a>硬件资源





硬件资源是可分配的可寻址总线路径，它们允许外围设备和系统处理器相互通信。 硬件资源通常包括 i/o 端口地址、中断向量和总线相关内存地址块。

在系统可以与*设备实例*通信之前，PnP 管理器必须根据可用资源和设备实例可以使用的资源，将硬件资源分配给设备实例。 将资源分配给[设备树](device-tree.md)中的每个设备节点（假设设备需要资源，而这些资源可用）。 PnP 管理器使用列表跟踪硬件资源，并将其与设备节点相关联。 它使用两种类型的列表：

<a href="" id="resource-requirements-list"></a>*资源要求列表*  
设备通常设计为在资源分配范围内运行。 例如，设备可能只需要一个中断向量，但它可以使用任何一种向量。 对于每个设备实例，PnP 管理器将维护一个*资源要求列表*，该列表指定设备可在其中运行的所有硬件资源范围。 列表的名称源自这样一个事实： PnP 管理器需要在将资源分配给设备时从此列表中选择资源。

内核模式代码使用[**IO\_资源\_需求\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_requirements_list)结构指定资源需求列表（作为系统例程的输入或响应 irp）。 用户模式代码指定资源需求列表，其中使用[pnp 配置管理器结构](https://docs.microsoft.com/previous-versions/ff549718(v=vs.85))作为[pnp 配置管理器功能](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))的输入。

<a href="" id="resource-list"></a>*资源列表*  
PnP 管理器将资源分配到设备时，会通过为每个设备实例创建分配的资源列表来跟踪这些分配。 这些列表可以称为*资源分配列表*，但该名称通常与*资源列表*短路。 在将设备添加到系统或从系统中删除资源时，PnP 管理器可以更改资源列表内容，并且随后会重新分配资源。 （也可以通过 PnP BIOS 分配资源。 另外，安装软件（使用 INF 文件或用户输入）可以强制 PnP 管理器将特定资源分配给设备。）

内核模式代码通过使用[**CM\_资源\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list)结构（作为系统例程的输入或响应 irp）来指定资源列表。 用户模式代码使用[pnp 配置管理器结构](https://docs.microsoft.com/previous-versions/ff549718(v=vs.85))指定资源列表作为[PnP 配置管理器功能](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))的输入。

PnP 管理器将资源需求列表和资源列表存储在注册表中，可以使用 Regedit.exe 来查看这些列表和资源列表。 驱动程序可以通过[即插即用例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)和[即插即用次要 irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)来间接访问这些列表。 用户模式应用程序可以使用[PnP 配置管理器功能](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))。 （驱动程序和应用程序不能使用注册表功能直接访问这些列表，因为在将来的版本中，存储格式可能会更改。）

### <a href="" id="ddk-logical-configurations-kg"></a>逻辑配置

资源需求列表和资源列表都包含一个或多个*逻辑配置*。 每个逻辑配置标识一系列可接受的资源或特定*设备实例*的一组特定资源。 此外，设备实例的每个逻辑配置属于一种*逻辑配置类型*。 下面列出了配置类型。 可能会将多个不同类型的逻辑配置分配给每个设备实例。

### <a name="logical-configuration-types-for-resource-requirements-lists"></a>资源需求列表的逻辑配置类型

<a href="" id="basic-configuration"></a>*基本配置*  
资源需求列表标识由即插即用设备提供的资源范围。 当驱动程序收到[**IRP\_MN\_QUERY\_资源\_要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements)IRP 时，驱动程序应返回此列表。 （可在 INF 文件中描述非 PnP 设备的基本配置。 在这种情况下，设备安装软件将读取 INF 文件并调用[PnP 配置管理器功能](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))以创建要求列表。）

<a href="" id="filtered-configuration"></a>*筛选的配置*  
为了响应[**IRP\_MN\_筛选器\_资源\_要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements)IRP，已提供到驱动程序堆栈的资源要求列表（可能已修改），然后由驱动程序堆栈返回。 PnP 管理器使用生成的筛选配置作为分配资源的基础。

<a href="" id="override-configuration"></a>*替代配置*  
替代基本配置的资源要求列表。 通常，如果设备的 INF 文件包含[**INF DDInstall. LogConfigOverride 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-logconfigoverride-section)，则设备安装程序会创建替代配置。 如果重写配置的设备从系统中被物理删除，则不会将其删除。

### <a name="logical-configuration-types-for-resource-lists"></a>资源列表的逻辑配置类型

<a href="" id="boot-configuration"></a>*启动配置*  
标识系统启动时分配给设备实例的资源的资源列表。 （对于 PnP 设备，这是 BIOS 提供的配置; 对于非 PnP 设备，可以通过卡上的跳线选择这些资源。）当驱动程序收到[**IRP\_MN\_QUERY\_资源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources)IRP 时，驱动程序应返回此资源列表。 （如果 BIOS 无法确定设备使用的所有资源，则启动配置可以部分为空。）如果删除或重新启动了设备，PnP 管理器可以修改此列表。 对于非 PnP 设备，可以使用此配置类型，而不是强制配置，在这种情况下，其配置优先级低于等效的强制配置。 每个设备实例只能有一个启动配置。

<a href="" id="forced-configuration"></a>*强制配置*  
标识设备实例必须使用的资源的资源列表。 强制配置可防止 PnP 管理器将其他资源分配给设备实例。 设备安装程序可能会基于包含在 INF 中或从用户接收的信息创建强制配置。 如果从系统中物理删除了强制配置，则不会将其删除。 每个设备实例只能有一个强制配置。

<a href="" id="allocated-configuration"></a>*分配的配置*  
标识设备实例当前正在使用的资源的资源列表。 每个设备实例只能有一个已分配的配置。

设备驱动程序负责确定与 PnP 兼容的设备的基本配置、筛选的配置和启动配置，并为响应 PnP 管理器发送的 Irp 而返回该信息。 （有关详细信息，请参阅向[正在运行的系统中添加 PnP 设备](adding-a-pnp-device-to-a-running-system.md)。）驱动程序安装软件可以为非 PnP 设备创建替代配置、强制配置和启动配置。 PnP 管理器维护每个设备实例的分配配置。

创建每个配置时，会为每个配置分配一个优先级。 如果 PnP 管理器发现已为某个设备实例分配了多个相同类型的逻辑配置，则会先尝试使用优先级最高的逻辑配置。 如果该配置导致资源冲突，则会尝试下一个较低优先级的配置。 （有关配置优先级的列表，请参阅[**CM\_将\_空\_日志添加到会议\_** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_add_empty_log_conf)。）

 

 




