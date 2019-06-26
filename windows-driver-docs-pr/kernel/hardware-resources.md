---
title: 硬件资源
description: 硬件资源
ms.assetid: c7a6997b-34f9-4dd9-b384-2321a8b5ce54
keywords:
- 资源描述符 WDK 即插即用
- 即插即用 WDK 内核，硬件资源
- 插 WDK 内核，硬件资源
- 资源要求列表 WDK 即插即用
- 资源列出了 WDK 即插即用
- 已分配资源 WDK 即插即用
- 要求列出了 WDK 即插即用
- 注册表 WDK 即插即用
- 逻辑配置 WDK 即插即用
- 启动配置 WDK 即插即用
- 强制的配置 WDK 即插即用
- 筛选的配置 WDK 即插即用
- 重写配置 WDK 即插即用
- 配置类型 WDK 即插即用
- 分配配置 WDK 即插即用
- 基本配置 WDK 即插即用
- 硬件资源
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d0872ce250ca7e0a48f4fa226452eb2a2942a712
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371881"
---
# <a name="hardware-resources"></a>硬件资源





硬件资源是允许外围设备和系统的处理器来相互通信的总线分配、 可寻址路径。 硬件资源通常包括 I/O 端口地址、 中断向量和总线相对内存地址的。

系统可以与进行通信之前*设备实例*，即插即用 manager 必须将硬件资源分配给基于知识提供了哪些资源，以及哪些设备实例是能够使用的设备实例. 资源分配给每个设备节点[设备树](device-tree.md)（假设表示的设备所需的资源，并提供了这些资源）。 跟踪使用列表，它将与设备节点相关联的硬件资源的即插即用管理器。 它使用两种类型的列表：

<a href="" id="resource-requirements-list"></a>*资源要求列表*  
设备通常用于在资源分配的范围内进行操作。 例如，设备可能需要只有一个中断矢量，但它可能能够使用任何一种矢量的范围。 对于每个设备实例，即插即用管理器将保留*资源要求列表*，它指定所有设备都可以在其中操作的硬件资源的范围。 从这一事实，即插即用管理器是需要从此列表中选择资源时将其分配给设备的词干提取列表的名称。

内核模式代码指定资源要求列出了使用[ **IO\_资源\_要求\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_resource_requirements_list)结构 （无论是作为系统例程的输入或响应 Irp）。 用户模式代码指定资源要求列出了使用[PnP 配置管理器的结构](https://docs.microsoft.com/previous-versions/ff549718(v=vs.85))到作为输入[PnP 配置管理器函数](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))。

<a href="" id="resource-list"></a>*资源列表*  
当 PnP 管理器将资源分配给设备时，它会跟踪的这些分配通过创建的已分配资源的每个设备实例列表。 无法调用这些列表*资源分配列表*，但该名称通常为短路*资源列表*。 PnP 管理器可以更改资源列出内容，如设备添加到或从系统中删除并随后重新分配资源。 （资源还可以分配由即插即用 BIOS。 此外，安装软件 — 使用 INF 文件或用户输入，可以强制 PnP 管理器中，若要将特定的资源分配到设备。)

内核模式代码通过使用指定资源列表[ **CM\_资源\_列表**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_cm_resource_list)结构 （无论是作为输入系统例程或 Irp 响应）。 用户模式代码指定资源列出了使用[PnP 配置管理器的结构](https://docs.microsoft.com/previous-versions/ff549718(v=vs.85))到作为输入[PnP 配置管理器函数](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))。

PnP 管理器存储在注册表中，其中他们可以通过 Regedit.exe 查看的资源要求列表和资源的列表。 驱动程序可以访问间接通过这些列表[即插即用例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)并[即插即用和播放次要 Irp](https://docs.microsoft.com/windows-hardware/drivers/kernel/plug-and-play-minor-irps)。 用户模式应用程序可以使用[PnP 配置管理器函数](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))。 （驱动程序和应用程序必须直接访问使用注册表函数，因为存储格式将在未来版本中进行这些列表。）

### <a href="" id="ddk-logical-configurations-kg"></a>逻辑配置

资源要求列表和资源列表包含一个或多个*逻辑配置*。 每个逻辑配置标识是一系列可接受的资源或一组特定资源的特定*设备实例*。 此外，设备实例的每个逻辑配置属于的某个*逻辑配置类型*。 下面列出了配置类型。 相同或不同类型的多个逻辑的配置可能会分配给每个设备。

### <a name="logical-configuration-types-for-resource-requirements-lists"></a>资源要求列表的逻辑配置类型

<a href="" id="basic-configuration"></a>*基本配置*  
资源要求列出标识由插设备提供的资源范围。 驱动程序应返回此列表，当它收到[ **IRP\_MN\_查询\_资源\_要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resource-requirements) IRP。 （非 PnP 设备的基本配置可以在 INF 文件中所述。 这种情况下，设备安装软件读取的 INF 文件和调用[PnP 配置管理器函数](https://docs.microsoft.com/previous-versions/ff549713(v=vs.85))创建要求列表。)

<a href="" id="filtered-configuration"></a>*筛选后的配置*  
资源要求列表，已提供给驱动程序堆栈，可能已经过修改，然后返回的驱动程序堆栈，以响应[ **IRP\_MN\_筛选器\_资源\_要求**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-filter-resource-requirements) IRP。 PnP 管理器使用生成的筛选的配置的基础分配资源。

<a href="" id="override-configuration"></a>*替代配置*  
资源要求列表，以替代基本配置。 通常情况下，设备安装程序创建替代的配置，如果设备的 INF 文件包含[ **INF DDInstall.LogConfigOverride 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-logconfigoverride-section)。 如果以物理方式从系统中删除其设备不会删除重写配置。

### <a name="logical-configuration-types-for-resource-lists"></a>资源列出的逻辑配置类型

<a href="" id="boot-configuration"></a>*启动配置*  
标识系统启动时分配给设备实例的资源的资源列表。 （对于即插即用设备，这是由 BIOS 提供的配置; 对于非 PnP 设备，这些资源可能会选择通过跳线在卡上。）驱动程序应返回此资源的列表，当它收到[ **IRP\_MN\_查询\_资源**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-resources) IRP。 （引导配置可以是 BIOS 无法确定设备使用的所有资源部分为空。）如果删除或重新启动设备的即插即用的管理器可以修改此列表。 对于非 PnP 设备，而不是强制性配置可以使用此配置类型，这种情况下，它具有较低配置的优先级比等效强制配置。 只有一个引导配置可以为每个设备实例存在。

<a href="" id="forced-configuration"></a>*强制性的配置*  
标识设备实例必须使用的资源的资源列表。 强制的配置会阻止 PnP 管理器将其他资源分配到设备实例。 设备安装程序可能会创建强制性的配置基于 INF 中包含的或从用户接收到的信息。 如果以物理方式从系统中删除其设备不会删除强制的配置。 只有一个强制性的配置可以为每个设备实例存在。

<a href="" id="allocated-configuration"></a>*已分配的配置*  
通过设备实例标识当前正在使用的资源的资源列表。 只能为一个已分配的配置可以为每个设备实例存在。

设备驱动程序负责确定 PnP 兼容设备的基本配置、 筛选后的配置和启动配置，并为 Irp 的即插即用的管理器发送到响应中返回该信息。 (有关详细信息，请参阅[添加到运行系统的即插即用设备](adding-a-pnp-device-to-a-running-system.md)。)驱动程序安装软件都可以创建重写配置，强制配置，并为非 PnP 设备启动配置。 PnP 管理器维护每个设备实例的已分配的配置。

在创建时，优先级被分配给每个配置。 如果 PnP 管理器找到该设备实例已分配相同类型的多个逻辑配置，它将尝试先使用具有最高优先级的一个。 如果该配置会导致资源冲突，它将尝试使用下一个较低优先级的配置。 (有关配置优先级的列表，请参阅[ **CM\_添加\_空\_日志\_Conf**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_add_empty_log_conf)。)

 

 




