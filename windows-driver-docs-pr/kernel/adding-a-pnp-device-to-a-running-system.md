---
title: 将 PnP 设备添加到正在运行的系统
description: 将 PnP 设备添加到正在运行的系统
ms.assetid: 73d14ba1-6cf1-44eb-8a98-8c2fe44c11bb
keywords:
- 即插即用 WDK 内核，将设备添加到正在运行的系统
- 插 WDK 内核，将设备添加到正在运行的系统
- 添加到正在运行的系统的即插即用设备
- 枚举即插即用设备 WDK 即插即用
- 报告的即插即用设备
- devnodes WDK 即插即用
- 设备节点 WDK 即插即用
- 功能的驱动程序 WDK 即插即用
- 筛选器驱动程序 WDK 即插即用
- AddDevice 例程 WDK 即插即用
- WDK PnP Irp
- I/O 请求数据包 WDK 即插即用
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dab5a0072d9ef9b00423135984e745a9808d93e0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63365878"
---
# <a name="adding-a-pnp-device-to-a-running-system"></a>将 PnP 设备添加到正在运行的系统





本部分介绍的事件发生时系统会在配置的用户已添加到正在运行的计算机的即插即用设备的序列。 此讨论突出显示即插即用管理器、 总线驱动程序和枚举和配置新设备中的函数和筛选器驱动程序的角色。

在本文的大部分也是与配置计算机启动时存在的即插即用设备相关的。 具体而言，其驱动程序标记为服务的设备\_需\_INF 文件中的开始配置实质上是相同的方式是否设备动态添加或已在启动时存在。

下图显示的第一个步骤中配置设备，从开始，当用户插入到计算机的硬件。

![演示如何枚举和报告插设备的关系图](images/hotplug.png)

以下说明与上图中带圆圈的数字相对应：

1.  用户插入到一个可用的插槽的即插即用总线上的即插即用设备。

    在此示例中，用户插入 USB 主控制器上的中心即插即用 USB 游戏杆。 USB 集线器是总线即插即用设备，因为子设备可以连接到它。

2.  总线设备功能驱动程序确定新的设备为其总线上。

    该驱动程序如何确定这取决于总线体系结构。 对于某些总线，总线功能驱动程序接收新设备的热即插即用的通知。 如果在总线不支持热插拔通知，用户必须采取相应的措施，会导致要枚举的总线控制面板中。

    在此示例中，USB 总线支持热插拔通知，以便通知 USB 总线功能驱动程序，子项已更改。

3.  总线设备功能驱动程序通知即插即用管理器已更改其组子设备。

    功能驱动程序通过调用通知即插即用管理器[ **IoInvalidateDeviceRelations** ](https://msdn.microsoft.com/library/windows/hardware/ff549353)与*类型*的**BusRelations**。

4.  PnP 管理器将查询的总线驱动程序有关的总线上设备的新列表。

    PnP 管理器将发送[ **IRP\_MN\_查询\_设备\_关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)到总线的设备堆栈的请求。 **Parameters.QueryDeviceRelations.Type**值是**BusRelations**，，该值指示在总线上的即插即用的管理器要求的当前存在的设备的列表 (*总线关系*).

    PnP 管理器将 IRP 发送到总线的设备堆栈中的顶部驱动程序。 根据 PnP Irp 的规则，堆栈中的每个驱动程序处理 IRP，如果适用，并将传递到下一步的驱动程序 IRP。

5.  总线设备功能驱动程序处理 IRP。

    请参阅的参考页[ **IRP\_MN\_查询\_设备\_关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)有关处理此 IRP 的详细信息。

    在此示例中，USB 集线器驱动程序处理的中心此 IRP *FDO*。 中心驱动程序创建*PDO*游戏杆设备并在其随 IRP 返回子设备列表中包括指向游戏杆 PDO 的引用。

    USB 集线器的父总线驱动程序 （USB 主机控制器类/miniclass 驱动程序对） 完成 IRP，IRP 传输到设备堆栈通过任何[ *IoCompletion* ](https://msdn.microsoft.com/library/windows/hardware/ff548354)例程注册通过中心驱动程序。

请注意，总线函数驱动程序通过请求的即插即用的管理器查询有关其子设备的列表来报告其的子级列表中的更改。 得到**IRP\_MN\_查询\_设备\_关系**请求被总线设备的所有驱动程序。 通常，总线功能驱动程序是唯一的驱动程序来处理 IRP 和报表子级。 在某些设备的堆栈，总线筛选器驱动程序存在，并参与构造总线关系的列表。 一个示例是 ACPI，ACPI 设备的总线筛选器驱动程序作为附加。 在某些设备堆栈、 nonbus 筛选器驱动程序处理**IRP\_MN\_查询\_设备\_关系**请求中，但这并不常见。

此时，即插即用 manager 总线上具有设备的当前列表。 PnP 管理器然后确定是否任何设备新到达或已删除。 在此示例中，没有一台新设备。 下图显示了创建的新设备 devnode 和开始配置设备的即插即用管理器。

![说明创建新的即插设备 devnode 的关系图](images/credvnd.png)

以下说明与上图中带圆圈的数字相对应：

1.  即插即用 manager devnodes 为创建任何新的子设备在总线上。

    PnP 管理器将总线关系中返回的列表进行比较**IRP\_MN\_查询\_设备\_关系**中即插即用当前记录到总线的子项列表的 IRP设备目录树。 PnP 管理器创建的每个新设备 devnode 并启动删除处理的任何设备的已删除。

    在此示例中，没有一台新设备 （游戏杆），因此 PnP 管理器创建的游戏杆 devnode。 此时，已针对游戏杆的唯一驱动程序是在父 USB 集线器总线驱动程序，创建游戏杆的 PDO。 任何可选总线筛选器驱动程序也都会出现在设备堆栈，但总线筛选器驱动程序为简单起见，示例省略了。

    在上图中两个 devnodes 之间的宽箭头表示游戏杆 devnode 的 USB 集线器 devnode 子级。

2.  PnP 管理器收集有关新设备的信息，并开始配置设备。

    PnP 管理器将一系列 Irp 发送到设备堆栈来收集有关设备的信息。 此时，设备堆栈包含，创建的设备的父总线驱动程序和任何可选总线筛选器驱动程序的筛选器 DOs PDO。 因此，总线驱动程序和总线筛选器驱动程序是应对这些 Irp 的唯一驱动程序。 在此示例中，游戏杆设备堆栈中的唯一驱动程序是父总线驱动程序 USB 集线器驱动程序。

    PnP 管理器通过将 Irp 发送到设备堆栈收集的新设备有关的信息。 这些 Irp 如下所示：

    -   [**IRP\_MN\_查询\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff551679)，以下类型的硬件 Id 的每个单独 IRP:

        **BusQueryDeviceID**

        **BusQueryInstanceID**

        **BusQueryHardwareIDs**

        **BusQueryCompatibleIDs**

        **BusQueryContainerID**

    -   [**IRP\_MN\_查询\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff551664)

    -   [**IRP\_MN\_查询\_设备\_文本**](https://msdn.microsoft.com/library/windows/hardware/ff551674)，以下各项的每个单独 IRP:

        **DeviceTextDescription**

        **DeviceTextLocationInformation**

    -   [**IRP\_MN\_查询\_总线\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff551654)
    -   [**IRP\_MN\_查询\_资源**](https://msdn.microsoft.com/library/windows/hardware/ff551710)
    -   [**IRP\_MN\_查询\_资源\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff551715)

    PnP 管理器将发送 Irp 上面列出的处理新的即插即用设备，此阶段，但不是一定是按所列的顺序，因此不应造成会假设在其中发送 Irp 的顺序。 此外，您不应假定 PnP 管理器将发送上述 Irp。

    PnP 管理器会检查注册表，以确定是否在设备已安装在此计算机上以前。 PnP 管理器检查&lt;*枚举器*&gt;\\&lt;*deviceID* &gt;子项下设备**枚举**分支。 在此示例中，设备的新，并且必须配置"从零开始。"

3.  PnP 管理器将有关设备的信息存储在注册表中。

    在注册表**枚举**分支保留供操作系统组件，其布局会有所更改。 驱动程序编写人员必须使用系统例程来提取与驱动程序相关的信息。 不会访问**枚举**分支直接从驱动程序。 以下**枚举**会列出仅用于进行调试的信息。

    -   PnP 管理器为设备的枚举器创建一个用于设备的项下的子项。

        PnP 管理器创建名为一个子项**HKLM\\系统\\CurrentControlSet\\枚举\\**&lt;*枚举器*&gt; **\\** &lt; *deviceID*&gt;。 它会创建&lt;*枚举器*&gt;子项如果尚不存在。

        *枚举器*发现即插即用设备的组件基于即插即用硬件标准。 一个枚举器的任务由 PnP 管理器与合作关系中的即插即用总线驱动程序执行。 通常由其父总线驱动程序，如 PCI 或 PCMCIA 枚举设备。 某些设备通过总线筛选器驱动程序，如 ACPI 枚举。

    -   PnP 管理器创建一个用于设备的此实例的子项。

        如果**Capabilities.UniqueID**作为返回**TRUE**有关**IRP\_MN\_查询\_功能**，设备的唯一 ID 是在系统是唯一的。 如果没有，即插即用管理器修改 ID，以便它是唯一的系统范围。

        PnP 管理器创建名为一个子项**HKLM\\系统\\CurrentControlSet\\枚举\\**&lt;*枚举器*&gt; **\\** &lt; *deviceID* &gt; **\\** &lt; *instanceID*&gt;。

    -   PnP 管理器将有关设备的信息写入到的设备实例的子项。

        PnP 管理器存储信息，包括以下内容，如果它为设备提供：

        **DeviceDesc** — 从[ **IRP\_MN\_查询\_设备\_文本**](https://msdn.microsoft.com/library/windows/hardware/ff551674)

        **位置** — 从**IRP\_MN\_查询\_设备\_文本**

        **功能** — 从标志[ **IRP\_MN\_查询\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff551664)

        **UINumber** — 从**IRP\_MN\_查询\_功能**

        **HardwareID** — 从[ **IRP\_MN\_查询\_ID**](https://msdn.microsoft.com/library/windows/hardware/ff551679)

        **CompatibleIDs** — 从**IRP\_MN\_查询\_ID**

        **ContainerID** — 从**IRP\_MN\_查询\_ID**

        **LogConf\\BootConfig** — 从[ **IRP\_MN\_查询\_资源**](https://msdn.microsoft.com/library/windows/hardware/ff551710)

        **LogConf\\BasicConfigVector** — 从[ **IRP\_MN\_查询\_资源\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff551715)

此时，即插即用管理器已准备好定位功能驱动程序和筛选这些设备驱动程序，如果有的话。 （请参阅下图。）

![关系图演示如何查找函数和筛选器驱动程序](images/finddrv.png)

以下说明与上图中的带编号圆圈相对应：

1.  内核模式即插即用管理器协调与用户模式即插即用管理器和用户模式下安装程序组件，若要查找的函数和筛选器驱动程序设备，如果有的话。

    内核模式即插即用 manager 队列将事件与用户模式即插即用管理器中，确定需要安装的设备。 特权的用户登录之后，用户模式组件将继续进行查找驱动程序。 请参阅[设备安装概述](https://msdn.microsoft.com/library/windows/hardware/ff549455)有关安装程序组件中安装设备及其角色的信息。

2.  用户模式下安装组件直接内核模式即插即用管理器要加载的函数和筛选器驱动程序。

    用户模式组件回调到内核模式以获得驱动程序加载，从而导致他们[ *AddDevice* ](https://msdn.microsoft.com/library/windows/hardware/ff540521)要调用的例程。

下图显示了 PnP 管理器加载驱动程序 （如果适用），调用其*AddDevice*例程，并指定要启动设备的驱动程序。

![关系图演示如何调用 adddevice 例程并启动新的设备](images/addstart.png)

以下说明与上图中的带编号圆圈相对应：

1.  较低的筛选器驱动程序

    功能驱动程序将附加到设备堆栈之前，即插即用管理器将处理任何更低的筛选器驱动程序。 对于每个低筛选器驱动程序，即插即用管理器调用驱动程序的[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff544113)例程，如果尚未加载该驱动程序。 然后，即插即用管理器调用的驱动程序*AddDevice*例程。 在其*AddDevice*例程，筛选器驱动程序创建一个筛选器设备对象 （筛选器执行操作） 并将其附加到设备堆栈 ([**IoAttachDeviceToDeviceStack**](https://msdn.microsoft.com/library/windows/hardware/ff548300))。 后它会将其设备对象附加到设备堆栈，该驱动程序将执行相应作为驱动程序的设备上。

    在 USB 游戏杆示例中，没有为设备的一个较低的筛选器驱动程序。

2.  功能驱动程序

    附加任何较低的筛选器后，即插即用管理器将处理功能驱动程序。 PnP 管理器中调用函数驱动程序**DriverEntry**如果驱动程序还未加载并调用函数驱动程序的例程*AddDevice*例程。 功能驱动程序创建一个函数设备对象 (FDO)，并将其附加到设备堆栈。

    在此示例中，USB 游戏杆功能驱动程序是实际的驱动程序的一对： HID 类驱动程序和 HID miniclass 驱动程序。 两个驱动程序协同工作来充当功能驱动程序。 驱动程序对创建只有一个 FDO，并将其附加到设备堆栈。

3.  Upper 筛选器驱动程序

    附加功能驱动程序后，即插即用管理器将处理任何大写筛选器驱动程序。

    在此示例中，没有为设备的一个上限筛选器驱动程序。

4.  将资源分配和启动设备

    PnP 管理器将资源分配到设备，如果需要并颁发 IRP 以启动设备。

    -   分配的资源

        前面的配置过程中，即插即用管理器从设备的父总线驱动程序中收集设备的硬件资源要求。 在加载设备驱动程序的完整集后，即插即用管理器将发送[ **IRP\_MN\_筛选器\_资源\_要求**](https://msdn.microsoft.com/library/windows/hardware/ff550874)请求为设备堆栈中。 堆栈中的所有驱动程序有机会处理此 IRP 并修改设备的资源要求列表，如有必要。

        PnP 管理器将资源分配给该设备，如果设备需要任何，基于设备的要求和当前可用的资源。

        PnP 管理器可能需要重新排列现有设备以满足需求的新设备的资源分配。 此重新分配的资源称为"重新平衡"。 现有设备的驱动程序接收序列的停止和启动 Irp 期间重新平衡，但重新平衡必须对用户透明。

        在 USB 游戏杆的示例中，USB 的设备不需要的硬件资源以便 PnP 管理器设置为资源列表**NULL**。

    -   启动设备 (**IRP\_MN\_启动\_设备**)

        一旦 PnP 管理器中向资源分配到设备，会将发送[ **IRP\_MN\_启动\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551749)到设备堆栈的 IRP，若要指示要启动的驱动程序设备。

    设备启动后，即插即用管理器将三个详细 Irp 发送到设备的驱动程序：

    -   [**IRP\_MN\_查询\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff551664)

        在后开始 IRP 成功完成时，即插即用管理器发送另一个**IRP\_MN\_查询\_功能**IRP 到设备堆栈。 这些设备的所有驱动程序可以处理 IRP 的选择。 PnP 管理器将此 IRP 发送在此时间后附加的所有驱动程序和设备已启动，因为函数或筛选器驱动程序可能需要访问设备收集功能的信息。

    -   [**IRP\_MN\_QUERY\_PNP\_DEVICE\_STATE**](https://msdn.microsoft.com/library/windows/hardware/ff551698)

        此 IRP 到，例如，设备应不显示在设备管理器和热插拔程序等的用户界面中的报表，使驱动程序有机会。 这可用于在系统上存在但不可在的当前配置，如便携式计算机未插接时不可用的便携式计算机上的游戏端口的设备。

    -   [**IRP\_MN\_查询\_设备\_关系**](https://msdn.microsoft.com/library/windows/hardware/ff551670)总线关系

        PnP 管理器将发送此 IRP，以确定设备是否具有任何子设备。 如果是这样，即插即用管理器将每个子设备配置。

 
## <a name="using-guidpnplocationinterface"></a>使用 GUID_PNP_LOCATION_INTERFACE

GUID_PNP_LOCATION_INTERFACE 接口提供 SPDRP_LOCATION_PATHS Plug and Play (PnP) 设备的设备属性。

若要在您的驱动程序中实现此接口，处理与 InterfaceType IRP_MN_QUERY_INTERFACE IRP = GUID_PNP_LOCATION_INTERFACE。 您的驱动程序提供了指向包含该接口的单个例程的指针的 PNP_LOCATION_INTERFACE 结构的指针。 [PnpGetLocationString 例程](https://msdn.microsoft.com/library/windows/hardware/ff558811)提供设备的 SPDRP_LOCATION_PATHS 属性的特定于设备的一部分。



 




