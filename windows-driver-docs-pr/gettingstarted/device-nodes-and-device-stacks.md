---
title: 设备节点和设备堆栈
description: 在 Windows 中，设备由即插即用 (PnP) 设备树中的设备节点来表示。
ms.assetid: 7bf38b3b-72ba-461c-b9e2-68b697359b37
keywords:
- 设备节点
- 设备堆栈
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 693337e45cc83ba7443a1e0f1910aaa24c605591
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518124"
---
# <a name="device-nodes-and-device-stacks"></a>设备节点和设备堆栈


在 Windows 中，设备由即插即用 (PnP) 设备树中的设备节点来表示。 通常，向设备发送 I/O 请求时，一些驱动程序会帮助处理该请求。 这些驱动程序中的每一个都与一个设备对象相关联，这些设备对象在堆栈中进行排列。 设备对象的顺序与它们的关联驱动程序一起被称为设备堆栈。 每个设备节点都有自己的设备堆栈。

## <a name="span-iddevicenodesandtheplugandplaydevicetreespanspan-iddevicenodesandtheplugandplaydevicetreespanspan-iddevicenodesandtheplugandplaydevicetreespandevice-nodes-and-the-plug-and-play-device-tree"></a><span id="Device_nodes_and_the_Plug_and_Play_device_tree"></span><span id="device_nodes_and_the_plug_and_play_device_tree"></span><span id="DEVICE_NODES_AND_THE_PLUG_AND_PLAY_DEVICE_TREE"></span>设备节点和即插即用设备树


Windows 在称为*即插即用设备树*或简称为*设备树*的树结构中整理设备。 通常，设备树中的节点表示复合设备上的某个设备或单个函数。 但是，某些节点表示与物理设备无关联的软件组件。

设备树中的节点称为“设备节点”。 设备树的根节点称为“根设备节点”。 常规情况下，根设备节点绘制在设备树的底部，如下图所示。

![设备树的示意图，其中显示了设备节点](images/devicetree01.png)

设备树说明了 PnP 环境中固有的父/子关系。 设备树中的一些节点表示包含与之连接的子设备的总线。 例如，PCI 总线节点表示主板上的物理 PCI 总线。 在启动过程中，PnP 管理器请求 PCI 总线驱动程序枚举连接到 PCI 总线的设备。 这些设备用 PCI 总线节点的子节点表示。 在上图中，PCI 总线节点包含连接到 PCI 总线的一些设备的子节点，其中包括 USB 主控制器、音频控制器以及 PCI Express 端口。

连接到 PCI 总线的某些设备为总线本身。 PnP 管理器请求这些总线中的每一个都枚举与之连接的设备。 在上图中，我们可以看到音频控制器为一个包含与之连接的音频设备的总线。 我们可以看到 PCI Express 端口为一个包含与之连接的显示适配器的总线，该显示适配器为包含一个与之连接的监视器的总线。

将节点视为表示设备还是总线取决于你的观点。 例如，你可以将显示适配器视为在准备将帧显示在屏幕上时扮演重要角色的设备。 但是，你也可以将显示适配器视为可以检测和枚举所连接监视器的总线。

## <a name="span-iddeviceobjectsanddevicestacksspanspan-iddeviceobjectsanddevicestacksspanspan-iddeviceobjectsanddevicestacksspandevice-objects-and-device-stacks"></a><span id="Device_objects_and_device_stacks"></span><span id="device_objects_and_device_stacks"></span><span id="DEVICE_OBJECTS_AND_DEVICE_STACKS"></span>设备对象和设备堆栈


“设备对象”是 [**DEVICE\_OBJECT**](https://msdn.microsoft.com/library/windows/hardware/ff543147) 结构的实例。 PnP 设备树中的每个设备节点都有设备对象的有序列表，这些设备对象中的每一个都与一个驱动程序相关联。 设备对象的有序列表与它们的关联驱动程序一起被称为设备节点的“设备堆栈”。

你可以采用多种方式考虑设备堆栈。 就最正式的意义而言，设备堆栈为（设备对象、驱动程序）对的有序列表。 但是，在某些上下文中，将设备堆栈视为设备对象的有序列表可能会有用。 在其他上下文中，将设备堆栈视为驱动程序的有序列表可能会有用。

常规情况下，设备堆栈具有顶部和底部。 在设备堆栈中创建的第一个设备对象位于底部，创建并附加到设备堆栈的最后一个设备对象位于顶部。

在下图中，Proseware Gizmo 设备节点的设备堆栈包含三个（设备对象、驱动程序）对。 顶部设备对象与驱动程序 AfterThought.sys 关联，中间的设备对象与驱动程序 Proseware.sys 关联，底部的设备对象与驱动程序 Pci.sys 关联。 图中心的 PCI 总线节点的设备堆栈包含两个（设备对象、驱动程序）对，一个设备对象与 Pci.sys 关联，一个设备对象与 Acpi.sys 关联。

![一个示意图，其中显示了 proseware gizmo 和 pci 设备节点的设备堆栈中有序设备对象](images/prosewaredevicenode01.png)

## <a name="span-idhowdoesadevicestackgetconstructedspanspan-idhowdoesadevicestackgetconstructedspanspan-idhowdoesadevicestackgetconstructedspanhow-does-a-device-stack-get-constructed"></a><span id="How_does_a_device_stack_get_constructed_"></span><span id="how_does_a_device_stack_get_constructed_"></span><span id="HOW_DOES_A_DEVICE_STACK_GET_CONSTRUCTED_"></span>如何构建设备堆栈？


在启动过程中，PnP 管理器请求每个总线的驱动程序枚举连接到该总线的子设备。 例如，PnP 管理器请求 PCI 总线驱动程序 (Pci.sys) 枚举连接到该 PCI 总线的设备。 为了响应此请求，Pci.sys 会为连接到 PCI 总线的每个设备创建一个设备对象。 这些设备对象中的每一个都被称为“物理设备对象”(PDO)。 在 Pci.sys 创建该组 PDO 不久之后，设备树类似于下图中的一个设备树。

![一个示意图，其中显示了 pci 节点和子设备的物理设备对象](images/prosewaredevicenode04.png)

PnP 管理器将设备节点与每个新创建的 PDO 关联，并查询注册表以确定哪些驱动程序需要成为该节点设备堆栈的一部分。 设备堆栈必须有且只有一个“函数驱动程序”，并且可以选择具有一个或多个“筛选器驱动程序”。 函数驱动程序为设备堆栈的主要驱动程序且负责处理读、写以及设备控制请求。 筛选器驱动程序在处理读、写以及设备控制请求中扮演辅助角色。 加载每个函数驱动程序和筛选器驱动程序时，它都会创建一个设备对象并将其自身附加到设备堆栈。 由函数驱动程序创建的设备对象称为“函数设备对象”(FDO)，由筛选器驱动程序创建的设备对象称为“筛选器设备对象”（筛选器 DO）。 现在设备树类似于此图。

![显示 proseware gizmo 设备节点中筛选器、函数以及物理设备对象的设备树图](images/prosewaredevicenode02.png)

在该图中，注意在一个节点中，筛选器驱动程序位于函数驱动程序之上，而在另一节点中，筛选器驱动程序位于函数驱动程序之下。 在设备堆栈中位于函数驱动程序之上的筛选器驱动程序称为“上筛选器驱动程序”。 位于函数驱动程序之下的筛选器驱动程序称为“下筛选器驱动程序”。

PDO 始终为设备堆栈中的底部设备对象。 这缘于设备堆栈的构造方式。 PDO 最先创建，并且当其他设备对象附加到堆栈中时，这些对象会附加到现有堆栈的顶部。

**注意**   安装设备驱动程序后，安装程序使用信息 (INF) 文件中的信息来确定哪个驱动程序为函数驱动程序，哪些驱动程序为筛选器。 通常，INF 文件由 Microsoft 或硬件供应商提供。 安装设备驱动程序后，PnP 管理器可以通过查找注册表来确定设备的函数驱动程序和筛选器驱动程序。

 

## <a name="span-idbusdriversspanspan-idbusdriversspanspan-idbusdriversspanbus-drivers"></a><span id="Bus_drivers"></span><span id="bus_drivers"></span><span id="BUS_DRIVERS"></span>总线驱动程序


在上图中，你可以看到驱动程序 Pci.sys 扮演两个角色。 第一，Pci.sys 与 PCI 总线设备节点中的 FDO 关联。 事实上，Pci.sys 已在 PCI 总线设备节点中创建 FDO。 因此，Pci.sys 为 PCI 总线的函数驱动程序。 第二，Pci.sys 与 PCI 总线节点的每个子节点中的 PDO 关联。 谨记 Pci.sys 已为子设备创建 PDO。 为设备节点创建 PDO 的驱动程序称为该节点的“总线驱动程序”。

如果你的参考点为 PCI 总线，则 Pci.sys 为函数驱动程序。 但如果你的参考点为 Proseware Gizmo 设备，则 Pci.sys 为总线驱动程序。 此双重角色为 PnP 设备树中的典型角色。 作为总线的函数驱动程序的驱动程序也是总线子设备的总线驱动程序。

## <a name="span-iduser-modedevicestacksspanspan-iduser-modedevicestacksspanspan-iduser-modedevicestacksspanuser-mode-device-stacks"></a><span id="User-mode_device_stacks"></span><span id="user-mode_device_stacks"></span><span id="USER-MODE_DEVICE_STACKS"></span>用户模式设备堆栈


到目前为止，我们已介绍了内核模式设备堆栈。 即，堆栈中的驱动程序在内核模式下运行，设备对象映射到系统空间，该空间是唯一一个以内核模式运行的代码能够使用的地址空间。 有关内核模式与用户模式之间差异的信息，请参阅[用户模式和内核模式](user-mode-and-kernel-mode.md)。

在某些情形下，设备不仅具有内核模式设备堆栈，同时还有用户模式设备堆栈。 用户模式驱动程序通常基于用户模式驱动程序框架 (UMDF)，它是 [Windows 驱动程序框架 (WDF)](https://docs.microsoft.com/windows-hardware/drivers/wdf/) 提供的驱动程序模型之一。 在 UMDF 中，驱动程序为用户模式 DLL，设备对象为实现 IWDFDevice 接口的 COM 对象。 UMDF 设备堆栈中的设备对象称为“WDF 设备对象”(WDF DO)。

下图显示了设备节点、内核模式设备堆栈以及 USB-FX-2 设备的用户模式设备堆栈。 用户模式和内核模式堆栈中的驱动程序参与在 USB-FX-2 设备上定向的 I/O 请求。

![一个示意图，其中显示了用户模式和内核模式设备堆栈](images/userandkerneldevicestacks01.png)

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[适用于所有驱动程序开发人员的概念](concepts-and-knowledge-for-all-driver-developers.md)

[驱动程序堆栈](driver-stacks.md)

 

 






