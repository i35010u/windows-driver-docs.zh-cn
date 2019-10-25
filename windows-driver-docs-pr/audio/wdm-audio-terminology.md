---
title: WDM 音频术语
description: WDM 音频术语
ms.assetid: bb36a66a-84dc-46c2-adcb-761d0acec3a1
keywords:
- WDM 音频驱动程序 WDK，关于 WDM 音频驱动程序
- 音频驱动程序 WDK，关于音频驱动程序
- 通用驱动程序体系结构 WDK 音频
- 微型端口驱动程序 WDK 音频、泛型与 WDM 音频
- 端口驱动程序 WDK 音频、泛型与 WDM 音频
- 微型驱动程序 WDK 音频
- 总线驱动程序 WDK 音频
- 适配器驱动程序 WDK 音频
- 类驱动程序 WDK 音频
- 上边缘接口 WDK 音频
- 较低边缘接口 WDK 音频
- 堆积 WDK 音频
- 驱动程序堆栈 WDK 音频
- 系统总线驱动程序 WDK 音频
- subdevices WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 01113712ce5c9c9aa67e1b90f4e832cb0493f3c9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72832247"
---
# <a name="wdm-audio-terminology"></a>WDM 音频术语


## <span id="wdm_audio_terminology"></span><span id="WDM_AUDIO_TERMINOLOGY"></span>


本部分介绍 Microsoft Windows 驱动模型（WDM）音频驱动程序体系结构和通用 Windows 分层驱动程序体系结构之间的术语差别。 一般的驱动程序体系结构由 SCSI 端口/微型端口驱动程序举例说明（请参阅[存储驱动程序体系结构](https://docs.microsoft.com/windows-hardware/drivers/storage/storage-driver-architecture)）。

一般和 WDM 音频驱动程序体系结构所定义的术语是相似的，但它们有一些重要的差异，如下所述。

### <a name="span-idminiport_driver__generic_spanspan-idminiport_driver__generic_spanspan-idminiport_driver__generic_spanminiport-driver-generic"></a><span id="Miniport_Driver__Generic_"></span><span id="miniport_driver__generic_"></span><span id="MINIPORT_DRIVER__GENERIC_"></span>微型端口驱动程序（通用）

微型端口驱动程序（通用）是位于系统总线上的适配器的特定于硬件的驱动程序（例如，PCI 或 ISA）。 此驱动程序有一个入口点， [*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)，并向端口驱动程序注册一个表。 此表可用作微型端口驱动程序的上边缘接口。

小型端口驱动程序位于驱动程序堆栈中的端口驱动程序下。 也就是说，对微型端口驱动程序的所有调用都是从端口驱动程序中进行的，而微型端口驱动程序的所有调用都是端口驱动程序的较小边缘接口。

下图说明了在此上下文中使用字词*堆栈*、*上边缘接口*和*更低边缘接口*时的含义。 表示端口驱动程序的块堆积在代表微型端口驱动程序的块的顶部。 因此，小型端口驱动程序位于 "堆栈" 中的端口驱动程序下。

![阐释驱动程序堆栈术语的关系图](images/drvstack.png)

端口和微型端口驱动程序通过它们相互公开的软件接口进行通信。 在上图中，这些接口与表示端口驱动程序的块的下边缘以及表示微型端口驱动程序的块的上边缘关联。 此表示形式是术语 "下边缘接口" 和 "边界接口" 的源。

### <a name="span-idport_driver__generic_spanspan-idport_driver__generic_spanspan-idport_driver__generic_spanport-driver-generic"></a><span id="Port_Driver__Generic_"></span><span id="port_driver__generic_"></span><span id="PORT_DRIVER__GENERIC_"></span>端口驱动程序（通用）

端口驱动程序（通用）围绕微型端口驱动程序。

端口驱动程序：

-   实现 WDM 流式处理筛选器。

-   为操作系统的其余部分提供公共接口。

-   处理从系统发出的 i/o 请求，并将这些请求 recasts 为调用微型端口驱动程序的函数表。

-   为微型端口驱动程序提供支持功能库（端口驱动程序的较小边缘界面）。

端口驱动程序将从微型端口驱动程序中隐藏操作系统的很多详细信息，微型端口驱动程序将从端口驱动程序中隐藏底层硬件的细节。 对于不同的操作系统版本，端口驱动程序的实现可能会发生变化，但端口驱动程序对小型端口驱动程序的接口会保持不变，使微型端口驱动程序可以在很大程度上独立于平台。

### <a name="span-idminidriver__generic_spanspan-idminidriver__generic_spanspan-idminidriver__generic_spanminidriver-generic"></a><span id="Minidriver__Generic_"></span><span id="minidriver__generic_"></span><span id="MINIDRIVER__GENERIC_"></span>微型驱动程序（通用）

微型驱动程序（通用）表示总线上的硬件组件。 微型驱动程序使用总线驱动程序通过总线与物理设备通信，并将总线驱动程序和一个或多个类驱动程序绑定在一起。

*类驱动程序*可帮助微型驱动程序将物理设备以一种逻辑设备的形式提供给客户端。 在 WDM 环境中，微型驱动程序通常从类驱动程序以 IRP 形式接收请求，并将 IRP 格式的请求发送到总线驱动程序。

微型驱动程序可能还必须与多个类驱动程序通信。 绑定到多个类驱动程序的微型驱动程序的一个示例是 IEEE 1394 总线上 CD-ROM 驱动器的微型驱动程序。 它可能绑定到文件系统驱动程序，以便可以从文件系统访问驱动器。 但是，它还绑定到[Redbook 系统驱动程序](kernel-mode-wdm-audio-components.md#redbook_system_driver)，以便可以从 cd 流式传输音频。

### <a name="span-idbus_driver__generic_spanspan-idbus_driver__generic_spanspan-idbus_driver__generic_spanbus-driver-generic"></a><span id="Bus_Driver__Generic_"></span><span id="bus_driver__generic_"></span><span id="BUS_DRIVER__GENERIC_"></span>总线驱动程序（通用）

总线驱动程序（通用）提供对物理总线的微型驱动程序访问。 Microsoft Windows*硬件抽象层（HAL）* 有时称为*系统总线驱动程序*，因为它提供对系统总线的访问。 有关详细信息，请参阅[总线驱动程序](https://docs.microsoft.com/windows-hardware/drivers/kernel/bus-drivers)。

### <a name="span-idclass_driver__generic_spanspan-idclass_driver__generic_spanspan-idclass_driver__generic_spanclass-driver-generic"></a><span id="Class_Driver__Generic_"></span><span id="class_driver__generic_"></span><span id="CLASS_DRIVER__GENERIC_"></span>类驱动程序（通用）

类驱动程序（泛型）实现了在一类类似设备上通用的行为。

类驱动程序：

-   消除硬件特定驱动程序中的功能的重复。

-   不是特定于总线的。

-   不知道资源问题（例如，DMA 和中断）。

### <a name="span-idminiport_driver__wdm_audio_spanspan-idminiport_driver__wdm_audio_spanspan-idminiport_driver__wdm_audio_spanminiport-driver-wdm-audio"></a><span id="Miniport_Driver__WDM_Audio_"></span><span id="miniport_driver__wdm_audio_"></span><span id="MINIPORT_DRIVER__WDM_AUDIO_"></span>微型端口驱动程序（WDM 音频）

小型端口驱动程序（WDM 音频）为驻留在系统总线上的音频适配器卡上的函数实现特定于函数的接口。 微型端口驱动程序是适配器驱动程序的一个组件。 操作系统不会将其识别为驱动程序。 在这方面，音频微型端口驱动程序与通用微型端口驱动程序不同。

与通用微型端口驱动程序不同，音频微型端口驱动程序不实现[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)，未注册，也不完全依赖其各自的端口驱动程序来提供支持。 多个寻址多个函数的音频微型端口驱动程序可以链接到单个适配器驱动程序（并与单个设备对象相关联）。

### <a name="span-idadapter_driver__wdm_audio_spanspan-idadapter_driver__wdm_audio_spanspan-idadapter_driver__wdm_audio_spanadapter-driver-wdm-audio"></a><span id="Adapter_Driver__WDM_Audio_"></span><span id="adapter_driver__wdm_audio_"></span><span id="ADAPTER_DRIVER__WDM_AUDIO_"></span>适配器驱动程序（WDM 音频）

适配器驱动程序（WDM 音频）充当与给定适配器关联的所有微型端口驱动程序的容器。 此适配器驱动程序被操作系统识别为驱动程序，并且包含在其自己的 .sys 文件中。

音频适配器驱动程序由一组微型端口驱动程序和其他代码组成，用于解决初始化问题。 例如，适配器驱动程序实现[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)入口点。

### <a name="span-idport_driver__wdm_audio_spanspan-idport_driver__wdm_audio_spanspan-idport_driver__wdm_audio_spanport-driver-wdm-audio"></a><span id="Port_Driver__WDM_Audio_"></span><span id="port_driver__wdm_audio_"></span><span id="PORT_DRIVER__WDM_AUDIO_"></span>端口驱动程序（WDM 音频）

端口驱动程序（WDM 音频）代表微型端口驱动程序实现 KS 筛选器，并且在端口类驱动程序的上下文中运行。 端口驱动程序会将微型端口驱动程序的特定于函数的代码作为 KS 筛选器公开给系统，并负责实现与适配器无关的功能。

与通用端口驱动程序不同的是，音频端口驱动程序共享设备对象，因此以不同的方式实例化。 与通用端口驱动程序相比，音频端口驱动程序还比泛型类驱动程序更相似，因为它实现了预期的一类设备（不与总线无关）的行为。

### <a name="span-idport_class_driver__wdm_audio_spanspan-idport_class_driver__wdm_audio_spanspan-idport_class_driver__wdm_audio_spanport-class-driver-wdm-audio"></a><span id="Port_Class_Driver__WDM_Audio_"></span><span id="port_class_driver__wdm_audio_"></span><span id="PORT_CLASS_DRIVER__WDM_AUDIO_"></span>端口类驱动程序（WDM 音频）

端口类驱动程序（WDM 音频）用作端口驱动程序集合的容器，其中每个端口驱动程序都提供对不同类型的音频硬件功能的支持。 下图显示了音频端口类与适配器驱动程序之间的关系。

![说明音频端口类和适配器驱动程序之间的关系的关系图](images/wdmaumi.png)

适配器驱动程序管理可能包含多个不同硬件功能的适配器卡。 如上图所示，适配器驱动程序包含用于管理各种硬件功能的微型端口驱动程序。 同样，端口类驱动程序旨在为包含多个硬件功能的适配器提供支持。 端口类驱动程序为它支持的每个完善定义的函数类型提供端口驱动程序。 适配器驱动程序将特定函数的微型端口驱动程序绑定到该函数类型的相应端口驱动程序。 每个函数的端口驱动程序处理与使用该函数的 WDM 音频客户端的通信。 微型端口驱动程序包含用于管理该函数的所有硬件特定代码。

端口类驱动程序（WDM 音频）主要充当与单个设备对象相关联的多个 subdevices 的容器。 总线驱动程序为其枚举的每个即插即用（PnP）节点创建单个*物理设备对象（PDO）* 。

对于音频适配器，单个 PnP 节点通常包含多个音频功能。 若要将与节点相关联的各种函数作为不同设备公开，通常需要为适配器编写总线驱动程序。 总线驱动程序枚举硬件函数并创建相应的 PDOs。 在此方案中，一个或多个特定于函数的驱动程序需要绑定到 PDOs，并与总线驱动程序协商以访问适配器上的共享资源。

端口类驱动程序使用内核流式处理驱动程序公开单个设备对象的各个方面的能力，以使操作系统将设备识别为一组不同的 subdevices。

将引用字符串附加到设备名称以指定所需的 subdevice。 内核流式处理驱动程序根据此引用字符串分派创建 Irp。 创建文件对象后，内核流式处理驱动程序会提供以代表 subdevice 的文件对象为目标的 Irp 调度。 此外，端口类驱动程序还为打包 subdevices 实现了基于 COM 的模型。

适配器驱动程序实例化端口驱动程序和微型端口驱动程序，并通过将指向微型端口驱动程序的指针作为参数传递给端口驱动程序的初始化功能（请参阅[Subdevice 创建](subdevice-creation.md)中的代码示例）。 生成的端口/微型端口驱动程序堆栈构成一个 KS 筛选器，该筛选器表示端口类驱动程序支持的 subdevice 类型之一。

端口类驱动程序的[**PcRegisterSubdevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/portcls/nf-portcls-pcregistersubdevice)函数将注册 subdevice，系统的其余部分会将其视为一种设备。 端口驱动程序接收以设备对象为目标的创建 Irp，但仅适用于在其下注册了 subdevice 的引用字符串指定的那些 Irp。 端口驱动程序还会接收以与 subdevice 关联的文件对象为目标的 Irp。 端口驱动程序负责将 subdevice 的行为作为 KS 筛选器，并与微型端口驱动程序一起正确通信。

有关设计多功能音频卡驱动程序的详细信息，请参阅[多功能音频设备](multifunction-audio-devices.md)。

 

 




