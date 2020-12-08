---
title: 将 PnP 设备添加到正在运行的系统
description: 将 PnP 设备添加到正在运行的系统
keywords:
- PnP WDK 内核，将设备添加到运行系统
- 即插即用 WDK 内核，将设备添加到运行系统
- 正在将 PnP 设备添加到运行系统
- 枚举 PnP 设备 WDK PnP
- 报告 PnP 设备
- devnodes WDK PnP
- 设备节点 WDK PnP
- 函数驱动程序 WDK PnP
- 筛选器驱动程序 WDK PnP
- AddDevice 例程 WDK PnP
- Irp WDK PnP
- I/o 请求数据包 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d08ebd51ba341784427cc5dc4ee18f12daa4b9d4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836963"
---
# <a name="adding-a-pnp-device-to-a-running-system"></a>将 PnP 设备添加到正在运行的系统





本部分介绍当系统配置用户已添加到正在运行的计算机的 PnP 设备时发生的事件的顺序。 本讨论重点介绍在枚举和配置新设备时，PnP 管理器、总线驱动程序以及函数和筛选器驱动程序的角色。

此讨论中的大部分还与配置计算机启动时存在的 PnP 设备有关。 具体而言，其驱动程序在 \_ \_ INF 文件中标记为 "服务需求开始" 的设备在本质上是采用相同的方式配置的，无论是动态添加设备还是在启动时提供设备。

下图显示了配置设备的第一步，从用户将硬件插入计算机起。

![说明如何枚举和报告即插即用设备的示意图](images/hotplug.png)

以下说明与上图中的带圆圈数字相对应：

1.  用户将 PnP 设备插入 PnP 总线上的可用槽。

    在此示例中，用户将一个 PnP USB 游戏杆插入到 USB 主机控制器的集线器中。 USB 集线器是 PnP 总线设备，因为子设备可以连接到它。

2.  总线设备的函数驱动程序确定新设备在其总线上。

    驱动程序如何确定这一点取决于总线体系结构。 对于某些总线，总线函数驱动程序接收新设备的热插拔通知。 如果总线不支持热插拔通知，则用户必须在 "控制面板" 中采取适当的措施来枚举总线。

    在此示例中，USB 总线支持热插拔通知，因此 USB 总线的函数驱动程序会通知其子节点已更改。

3.  总线设备的函数驱动程序将通知 PnP 管理器其子设备集已更改。

    函数驱动程序通过调用 *类型* 为 **BusRelations** 的 [**IoInvalidateDeviceRelations**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicerelations)通知 PnP 管理器。

4.  PnP 管理器将在总线的驱动程序上查询总线上当前设备的列表。

    PnP 管理器将 [**IRP \_ MN \_ 查询 \_ 设备 \_ 关系**](./irp-mn-query-device-relations.md) 请求发送到总线的设备堆栈。 **QueryDeviceRelations** 值为 **BusRelations**，指示 PnP 管理器正在请求总线上存在的设备的当前列表 (*总线关系*) 。

    PnP 管理器将 IRP 发送到总线的设备堆栈中的顶层驱动程序。 根据 PnP Irp 的规则，堆栈中的每个驱动程序会根据需要处理 IRP，并将 IRP 向下传递到下一个驱动程序。

5.  总线设备的函数驱动程序处理 IRP。

    有关处理此 IRP 的详细信息，请参阅 [**IRP \_ MN \_ 查询 \_ 设备 \_ 关系**](./irp-mn-query-device-relations.md) 的参考页。

    在此示例中，USB 集线器驱动程序为中心 *FDO* 处理此 IRP。 集线器驱动程序为操纵杆设备创建一个 *PDO* ，并在其使用 IRP 返回的子设备列表中包含指向游戏杆 PDO 的引用指针。

    如果 USB 集线器的父总线驱动程序 (USB 主机控制器类/miniclass 驱动程序对) 完成 IRP，则 IRP 会通过集线器驱动程序注册的任何 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程来返回设备堆栈。

请注意，总线函数驱动程序通过请求 PnP 管理器查询其子设备列表中的子项列表来报告更改。 总线设备的所有驱动程序都可查看生成的 **IRP \_ MN \_ 查询 \_ 设备 \_ 关系** 请求。 通常，总线函数驱动程序是处理 IRP 和报表子项的唯一驱动程序。 在某些设备堆栈中，总线筛选器驱动程序存在，并参与构造总线关系的列表。 例如，ACPI 是 ACPI 设备的总线筛选器驱动程序。 在某些设备堆栈中，nonbus 筛选器驱动程序处理 **IRP \_ MN \_ 查询 \_ 设备 \_ 关系** 请求，但这并不是典型情况。

此时，PnP 管理器具有总线上设备的当前列表。 然后，PnP 管理器将确定是否有任何设备新近到达或已被删除。 在此示例中，有一个新的设备。 下图显示了为新设备创建 devnode 并开始配置设备的 PnP 管理器。

![说明如何为新的即插即用设备创建 devnode 的关系图](images/credvnd.png)

以下说明与上图中的带圆圈数字相对应：

1.  PnP 管理器为总线上的任何新子设备创建 devnodes。

    PnP 管理器将 **irp \_ MN \_ 查询 \_ 设备 \_ 关系** IRP 中返回的总线关系的列表与 pnp 设备树中当前记录的总线的子项列表进行比较。 PnP 管理器为每个新设备创建一个 devnode，并为已删除的任何设备启动删除处理。

    在此示例中，有一个新设备 (游戏杆) ，因此 PnP 管理器会为操纵杆创建一个 devnode。 此时，为操纵杆配置的唯一驱动程序为父 USB 集线器总线驱动程序，该驱动程序创建了操纵杆的 PDO。 任何可选的总线筛选器驱动程序也会出现在设备堆栈中，但该示例省略了总线筛选器驱动程序以简化。

    上图中两个 devnodes 之间的宽箭头表示操纵杆 devnode 是 USB 集线器 devnode 的子。

2.  PnP 管理器收集有关新设备的信息并开始配置设备。

    PnP 管理器将一系列 Irp 发送到设备堆栈以收集有关设备的信息。 此时，设备堆栈只包含设备的父总线驱动程序和筛选器 DOs （对于任何可选的总线筛选器驱动程序）创建的 PDO。 因此，总线驱动程序和总线筛选器驱动程序是响应这些 Irp 的唯一驱动程序。 在此示例中，游戏杆设备堆栈中唯一的驱动程序为父总线驱动程序，即 USB 集线器驱动程序。

    PnP 管理器通过将 Irp 发送到设备堆栈来收集有关新设备的信息。 这些 Irp 包括：

    -   [**IRP \_MN \_ 查询 \_ ID**](./irp-mn-query-id.md)，适用于以下每种类型的硬件 ID 的单独 IRP：

        **BusQueryDeviceID**

        **BusQueryInstanceID**

        **BusQueryHardwareIDs**

        **BusQueryCompatibleIDs**

        **BusQueryContainerID**

    -   [**IRP \_ MN \_ 查询 \_ 功能**](./irp-mn-query-capabilities.md)

    -   [**IRP \_MN \_ 查询 \_ 设备 \_ 文本**](./irp-mn-query-device-text.md)，为以下各项提供单独的 IRP：

        **DeviceTextDescription**

        **DeviceTextLocationInformation**

    -   [**IRP \_ MN \_ 查询 \_ 总线 \_ 信息**](./irp-mn-query-bus-information.md)
    -   [**IRP \_ MN \_ 查询 \_ 资源**](./irp-mn-query-resources.md)
    -   [**IRP \_ MN \_ 查询 \_ 资源 \_ 需求**](./irp-mn-query-resource-requirements.md)

    PnP 管理器将在处理新的 PnP 设备的这一阶段发送上面列出的 Irp，但不一定按列出的顺序进行操作，因此，不应对 Irp 的发送顺序作出假设。 此外，不应假定 PnP 管理器只发送以上列出的 Irp。

    PnP 管理器检查注册表以确定此计算机上是否已安装了该设备。 PnP 管理器 &lt; *enumerator* &gt; \\ &lt; *deviceID* &gt; 在 **枚举** 分支下检查设备的枚举器 deviceID 子项。 在此示例中，该设备是新设备，必须配置为 "从头开始"。

3.  PnP 管理器将有关设备的信息存储在注册表中。

    注册表的 **枚举** 分支保留供操作系统组件使用，其布局可能会更改。 驱动程序编写器必须使用系统例程来提取与驱动程序相关的信息。 不要直接从驱动程序访问 **枚举** 分支。 下面列出的 **枚举** 信息仅用于调试目的。

    -   PnP 管理器为设备的枚举器的密钥下的设备创建一个子项。

        PnP 管理器创建一个名为 **HKLM \\ System \\ CurrentControlSet \\ Enum \\** &lt; *枚举器* &gt; **\\** &lt; *deviceID* 的子项 &gt; 。 &lt;如果 *枚举器* &gt; 子项尚不存在，则创建它。

        *枚举器* 是基于 pnp 硬件标准发现 PnP 设备的组件。 枚举器的任务通过与 PnP 管理器合作的 PnP 总线驱动程序执行。 设备通常由其父总线驱动程序（如 PCI 或 PCMCIA）枚举。 某些设备由总线筛选器驱动程序（如 ACPI）枚举。

    -   PnP 管理器为设备的此实例创建子项。

        如果为 **IRP \_ MN \_ 查询 \_ 功能** 返回 **TRUE** **UniqueID** ，则设备的唯一 ID 在整个系统中是唯一的。 如果不是，则 PnP 管理器会修改 ID，使其在整个系统范围内是唯一的。

        PnP 管理器创建一个名为 **HKLM \\ System \\ CurrentControlSet \\ Enum \\** &lt; *枚举器* &gt; **\\** &lt; *deviceID* &gt; **\\** &lt; *instanceID* &gt; 的子项。

    -   PnP 管理器将有关设备的信息写入设备实例的子项。

        如果为设备提供了以下信息，则 PnP 管理器将存储信息，包括以下信息：

        **DeviceDesc** —从 [ **IRP \_ MN \_ 查询 \_ 设备 \_ 文本**](./irp-mn-query-device-text.md)

        **位置** -从 **IRP \_ MN \_ 查询 \_ 设备 \_ 文本**

        **功能**- [ **IRP \_ MN \_ 查询 \_ 功能** 的标志](./irp-mn-query-capabilities.md)

        **UINumber** —从 **IRP \_ MN \_ 查询 \_ 功能**

        **HardwareID** —从 [ **IRP \_ MN \_ 查询 \_ ID**](./irp-mn-query-id.md)

        **CompatibleIDs** —从 **IRP \_ MN \_ 查询 \_ ID**

        **ContainerID** -从 **IRP \_ MN \_ 查询 \_ ID**

        **LogConf \\BootConfig** —从 [ **IRP \_ MN \_ 查询 \_ 资源**](./irp-mn-query-resources.md)

        **LogConf \\BasicConfigVector** —从 [ **IRP \_ MN \_ 查询 \_ 资源 \_ 要求**](./irp-mn-query-resource-requirements.md)

此时，PnP 管理器准备好查找该设备的函数驱动程序和筛选器驱动程序（如果有）。  (参见下图。 ) 

![阐释查找函数和筛选器驱动程序的示意图](images/finddrv.png)

以下说明与上图中的带编号的圆圈相对应：

1.  内核模式 PnP 管理器与用户模式 PnP 管理器和用户模式安装组件协调，以便查找设备的函数和筛选器驱动程序（如果有）。

    内核模式 PnP 管理器将事件排队到用户模式 PnP 管理器，标识需要安装的设备。 当特权用户登录后，用户模式组件会继续查找驱动程序。 请参阅 [设备安装概述](../install/overview-of-device-and-driver-installation.md) ，了解有关安装组件及其在设备中的角色的信息。

2.  用户模式安装组件将内核模式 PnP 管理器定向到加载函数和筛选器驱动程序。

    用户模式组件会回叫内核模式以获取加载的驱动程序，从而导致调用其 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程。

下图显示了 "PnP 管理器" 加载驱动程序 (如果适当) 、调用其 *AddDevice* 例程，并定向驱动程序以启动设备。

![说明如何调用 adddevice 例程并启动新设备的关系图](images/addstart.png)

以下说明与上图中的带编号的圆圈相对应：

1.  较低筛选器驱动程序

    在将函数驱动程序附加到设备堆栈之前，PnP 管理器将处理所有较低级别的驱动程序。 对于每个小写筛选器驱动程序，如果尚未加载驱动程序，则 PnP 管理器会调用驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程。 然后，PnP 管理器调用驱动程序的 *AddDevice* 例程。 筛选器驱动程序在其 *AddDevice* 例程中创建筛选器设备对象 (filter) 并将其附加到设备堆栈 ([**IoAttachDeviceToDeviceStack**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioattachdevicetodevicestack)) 。 将设备对象附加到设备堆栈后，驱动程序将作为设备的驱动程序。

    在 USB 游戏杆示例中，设备有一个较低的筛选器驱动程序。

2.  函数驱动程序

    附加了任何较低级别的筛选器后，PnP 管理器将处理函数驱动程序。 如果尚未加载驱动程序并调用函数驱动程序的 *AddDevice* 例程，PnP 管理器将调用函数驱动程序的 **DriverEntry** 例程。 函数驱动程序创建 (FDO) 的函数设备对象，并将其附加到设备堆栈。

    在此示例中，USB 游戏杆的函数驱动程序实际上是一对驱动程序： HID 类驱动程序和 HID miniclass 驱动程序。 这两个驱动程序协同工作以充当函数驱动程序。 驱动程序对仅创建一个 FDO，并将其附加到设备堆栈。

3.  上限筛选器驱动程序

    附加函数驱动程序后，PnP 管理器将处理任何上层筛选器驱动程序。

    在此示例中，设备有一个上层筛选器驱动程序。

4.  分配资源和启动设备

    如果需要，PnP 管理器会将资源分配给设备，并发出 IRP 来启动设备。

    -   分配资源

        之前在配置过程中，PnP 管理器从设备的父总线驱动程序收集设备的硬件资源需求。 为设备加载完整的驱动程序集后，PnP 管理器会将 [**IRP \_ MN \_ 筛选器 \_ 资源 \_ 要求**](./irp-mn-filter-resource-requirements.md) 请求发送到设备堆栈。 如果需要，堆栈中的所有驱动程序都有机会处理此 IRP 并修改设备的资源需求列表。

        PnP 管理器根据设备的要求以及当前可用的资源，将资源分配给设备（如果设备需要）。

        PnP 管理器可能需要重新排列现有设备的资源分配，以满足新设备的需求。 资源的这一重新分配称为 "重新平衡"。 现有设备的驱动程序会在重新平衡过程中收到一系列停止和启动 Irp，但重新平衡必须对用户是透明的。

        在 USB 游戏杆的示例中，USB 设备不需要硬件资源，因此 PnP 管理器将资源列表设置为 **NULL**。

    -   启动设备 (**IRP \_ MN \_ START \_ device**) 

        一旦 PnP 管理器将资源分配给设备，则会将 [**irp \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md) irp 发送到设备堆栈，以指示驱动程序启动设备。

    设备启动后，PnP 管理器会将3个其他 Irp 发送到设备的驱动程序：

    -   [**IRP \_ MN \_ 查询 \_ 功能**](./irp-mn-query-capabilities.md)

        启动 IRP 成功完成后，PnP 管理器会将另一个 **IRP \_ MN \_ 查询 \_ 功能** irp 发送到设备堆栈。 设备的所有驱动程序都具有处理 IRP 的选项。 此时，PnP 管理器会在附加了所有驱动程序并启动了设备后发送此 IRP，因为函数或筛选器驱动程序可能需要访问设备以收集功能信息。

    -   [**IRP \_ MN \_ 查询 \_ PNP \_ 设备 \_ 状态**](./irp-mn-query-pnp-device-state.md)

        例如，此 IRP 为驱动程序提供了机会，以报告设备不应在用户界面（如设备管理器和热插拔程序）中显示。 这对于系统上存在但在当前配置中无法使用的设备十分有用，例如便携机断开连接时无法使用的便携式计算机上的游戏端口。

    -   [**IRP \_用于总线关系的 MN \_ 查询 \_ 设备 \_ 关系**](./irp-mn-query-device-relations.md)

        PnP 管理器发送此 IRP 来确定设备是否有任何子设备。 如果是这样，PnP 管理器将配置每个子设备。

 
## <a name="using-guid_pnp_location_interface"></a>使用 GUID_PNP_LOCATION_INTERFACE

GUID_PNP_LOCATION_INTERFACE 接口提供设备 (PnP) 设备属性的 SPDRP_LOCATION_PATHS 即插即用。

若要在你的驱动程序中实现此接口，请处理 IRP_MN_QUERY_INTERFACE IRP，其中 InterfaceType = GUID_PNP_LOCATION_INTERFACE。 驱动程序提供一个指向 PNP_LOCATION_INTERFACE 结构的指针，该结构包含指向接口的各个例程的指针。 [PnpGetLocationString 例程](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-pget_location_string)提供设备 SPDRP_LOCATION_PATHS 属性的设备特定部分。



