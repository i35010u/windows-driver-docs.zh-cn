---
title: WDM 音频术语
description: WDM 音频术语
ms.assetid: bb36a66a-84dc-46c2-adcb-761d0acec3a1
keywords:
- WDM 音频驱动程序 WDK，有关 WDM 音频驱动程序
- 有关音频驱动程序的音频驱动程序 WDK，
- 通用驱动程序体系结构 WDK 音频
- 微型端口驱动程序 WDK 音频的通用 vs。WDM 音频
- 端口驱动程序 WDK 音频的通用 vs。WDM 音频
- 微型驱动程序 WDK 音频
- 总线驱动程序 WDK 音频
- 适配器驱动程序 WDK 音频
- 类驱动程序 WDK 音频
- 上边缘接口 WDK 音频
- 较低边缘接口 WDK 音频
- 堆栈 WDK 音频
- 驱动程序堆栈 WDK 音频
- 系统总线驱动程序 WDK 音频
- 子设备 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4da081c1b5fcbe3f4e74a17a818e41a13552dcb3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328479"
---
# <a name="wdm-audio-terminology"></a>WDM 音频术语


## <span id="wdm_audio_terminology"></span><span id="WDM_AUDIO_TERMINOLOGY"></span>


本部分介绍在术语中的 Microsoft Windows 驱动程序模型 (WDM) 音频驱动程序体系结构和通用 Windows 分层驱动程序体系结构之间的差异。 SCSI 端口/微型端口驱动程序以为例通用驱动程序体系结构 (请参阅[存储驱动程序体系结构](https://msdn.microsoft.com/library/windows/hardware/ff566978))。

术语定义的泛型和 WDM 音频驱动程序体系结构类似，但它们具有一些重要的区别，如下所述。

### <a name="span-idminiportdrivergenericspanspan-idminiportdrivergenericspanspan-idminiportdrivergenericspanminiport-driver-generic"></a><span id="Miniport_Driver__Generic_"></span><span id="miniport_driver__generic_"></span><span id="MINIPORT_DRIVER__GENERIC_"></span>微型端口驱动程序 （通用）

微型端口驱动程序 （通用） 是驻留在系统总线 （例如，PCI 或 ISA） 上的适配器的特定于硬件的驱动程序。 此驱动程序具有单一入口点[ *DriverEntry*](https://msdn.microsoft.com/library/windows/hardware/ff544113)，并通过端口驱动程序注册的函数表。 此函数的表用作微型端口驱动程序的上边缘接口。

微型端口驱动程序位于驱动程序堆栈中的端口驱动程序的下方。 也就是说，到微型端口驱动程序的所有调用都都来自端口驱动程序和带微型端口驱动程序的所有调用都是到端口驱动程序的较低 edge 接口。

下图说明了这些术语的含义*堆栈*，*上边缘接口*，并*低 edge 接口*因为它们将在此上下文中使用。 表示端口驱动程序的块被堆积顶部表示微型端口驱动程序的块。 因此，微型端口驱动程序位于下方"堆栈"中的端口驱动程序。

![说明驱动程序堆栈术语的关系图](images/drvstack.png)

端口和微型端口驱动程序进行通信通过软件接口它们公开到对方。 在上图中，这些接口相关联的表示端口驱动程序和表示微型端口驱动程序块的上边缘的块的较低边缘。 这种表示形式是术语"较低边缘接口"和"上边缘接口"的源。

### <a name="span-idportdrivergenericspanspan-idportdrivergenericspanspan-idportdrivergenericspanport-driver-generic"></a><span id="Port_Driver__Generic_"></span><span id="port_driver__generic_"></span><span id="PORT_DRIVER__GENERIC_"></span>端口驱动程序 （通用）

端口驱动程序 （泛型） 会环绕微型端口驱动程序。

端口驱动程序：

-   实现 WDM 流式处理筛选器。

-   提供了操作系统的其余部分的常见界面。

-   处理来自系统的 I/O 请求，并作为微型端口驱动程序的函数表调用 recasts 这些请求。

-   提供的支持函数 （端口驱动程序的较低边缘接口） 库的微型端口驱动程序。

端口驱动程序隐藏许多详细信息的操作系统从微型端口驱动程序，并且微型端口驱动程序将隐藏来自端口驱动程序的基础硬件。 端口驱动程序的实现可能需要进行更改为不同的操作系统的版本中，但端口驱动程序的微型端口驱动程序接口仍然更超过的保持不变，启用将很大程度上独立于平台的微型端口驱动程序。

### <a name="span-idminidrivergenericspanspan-idminidrivergenericspanspan-idminidrivergenericspanminidriver-generic"></a><span id="Minidriver__Generic_"></span><span id="minidriver__generic_"></span><span id="MINIDRIVER__GENERIC_"></span>微型驱动程序 （通用）

微型驱动程序 （泛型） 表示的总线上的硬件组件。 微型驱动程序使用的总线驱动程序通过总线，到物理设备进行通信和总线驱动程序和一个或多个类驱动程序一起绑定。

*类驱动程序*帮助微型驱动程序作为逻辑设备的类型向客户端提供物理设备。 在 WDM 环境中，微型驱动程序通常在从类驱动程序的 IRP 窗体中接收请求并将 IRP 窗体中的请求发送到总线驱动程序。

微型驱动程序还可能与多个类驱动程序进行通信。 将绑定到多个类驱动程序微型驱动程序的一个示例是 IEEE 1394 总线上的 CD-ROM 驱动器微型驱动程序。 它可能会将绑定到的文件系统驱动程序，以便可以从文件系统访问驱动器。 但是，它还会将绑定到[Redbook 系统驱动程序](kernel-mode-wdm-audio-components.md#redbook_system_driver)，以便可以从 Cd 音频进行流式处理。

### <a name="span-idbusdrivergenericspanspan-idbusdrivergenericspanspan-idbusdrivergenericspanbus-driver-generic"></a><span id="Bus_Driver__Generic_"></span><span id="bus_driver__generic_"></span><span id="BUS_DRIVER__GENERIC_"></span>总线驱动程序 （通用）

总线驱动程序 （泛型） 使物理总线微型驱动程序访问。 Microsoft Windows*硬件抽象层 (HAL)* 有时称为*系统总线驱动程序*因为它提供对系统总线的访问。 有关详细信息，请参阅[总线驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540704)。

### <a name="span-idclassdrivergenericspanspan-idclassdrivergenericspanspan-idclassdrivergenericspanclass-driver-generic"></a><span id="Class_Driver__Generic_"></span><span id="class_driver__generic_"></span><span id="CLASS_DRIVER__GENERIC_"></span>类驱动程序 （通用）

（通用） 的类驱动程序实现类似的设备的类之间的行为。

类驱动程序：

-   消除重复的特定于硬件的驱动程序中的功能。

-   不是特定于总线的。

-   不能识别的资源问题 （例如，DMA 和中断）。

### <a name="span-idminiportdriverwdmaudiospanspan-idminiportdriverwdmaudiospanspan-idminiportdriverwdmaudiospanminiport-driver-wdm-audio"></a><span id="Miniport_Driver__WDM_Audio_"></span><span id="miniport_driver__wdm_audio_"></span><span id="MINIPORT_DRIVER__WDM_AUDIO_"></span>微型端口驱动程序 （WDM 音频）

微型端口驱动程序 （WDM 音频） 实现上驻留在系统总线的音频的适配器卡函数特定于函数的接口。 微型端口驱动程序是适配器驱动程序的组件。 它不是由操作系统识别作为驱动程序。 在这方面，音频微型端口驱动程序不同于一般的微型端口驱动程序。

与不同的是泛型的微型端口驱动程序音频微型端口驱动程序不会实现[ *DriverEntry*](https://msdn.microsoft.com/library/windows/hardware/ff544113)、 未注册，并不完全靠支持其相应端口驱动程序。 解决多个函数的多个音频微型端口驱动程序可以是链接到单个适配器驱动程序 （和与单个设备对象相关联）。

### <a name="span-idadapterdriverwdmaudiospanspan-idadapterdriverwdmaudiospanspan-idadapterdriverwdmaudiospanadapter-driver-wdm-audio"></a><span id="Adapter_Driver__WDM_Audio_"></span><span id="adapter_driver__wdm_audio_"></span><span id="ADAPTER_DRIVER__WDM_AUDIO_"></span>适配器驱动程序 （WDM 音频）

适配器驱动程序 （WDM 音频） 可用作所有与给定适配器关联的微型端口驱动程序的容器。 此适配器驱动程序由操作系统识别作为驱动程序，以及包含在其自己的.sys 文件。

音频适配器驱动程序包含一组的微型端口驱动程序和解决初始化问题的其他代码。 例如，适配器驱动程序实现[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)入口点。

### <a name="span-idportdriverwdmaudiospanspan-idportdriverwdmaudiospanspan-idportdriverwdmaudiospanport-driver-wdm-audio"></a><span id="Port_Driver__WDM_Audio_"></span><span id="port_driver__wdm_audio_"></span><span id="PORT_DRIVER__WDM_AUDIO_"></span>端口驱动程序 （WDM 音频）

端口驱动程序 （WDM 音频） 实现 KS 代表微型端口驱动程序筛选器，并在端口类驱动程序的上下文运行。 端口驱动程序微型端口驱动程序的特定于函数的代码公开作为到系统 KS 筛选器，负责实现独立于适配器的功能。

与泛型端口驱动程序，不同的音频端口驱动程序共享的设备对象和，因此，实例化以不同的方式。 音频端口驱动程序也是类的最为相似的泛型类驱动程序比泛型端口驱动程序，其中实现预期的设备 （它不是类的独立于总线的） 的行为。

### <a name="span-idportclassdriverwdmaudiospanspan-idportclassdriverwdmaudiospanspan-idportclassdriverwdmaudiospanport-class-driver-wdm-audio"></a><span id="Port_Class_Driver__WDM_Audio_"></span><span id="port_class_driver__wdm_audio_"></span><span id="PORT_CLASS_DRIVER__WDM_AUDIO_"></span>端口类驱动程序 （WDM 音频）

端口类驱动程序 （WDM 音频） 可用作一系列端口驱动程序，其中每个不同类型的音频硬件函数提供支持的容器。 下图显示了音频端口类和适配器驱动程序之间的关系。

![说明音频端口类和适配器驱动程序之间的关系的关系图](images/wdmaumi.png)

适配器驱动程序管理可能包含多个不同的硬件功能的适配器卡。 在上图中所示，适配器驱动程序包含微型端口驱动程序来管理每种类型的硬件函数。 同样，端口类驱动程序旨在与多个硬件函数提供适配器卡的支持。 端口类驱动程序提供了每个定义完善的函数类型，它支持端口驱动程序。 适配器驱动程序将其用于特定函数的微型端口驱动程序绑定到该函数类型的相应端口驱动程序。 每个函数的端口驱动程序处理与使用该函数的 WDM 音频客户端通信。 微型端口驱动程序包含的所有特定于硬件的代码，用于管理该函数。

端口类驱动程序 （WDM 音频） 的主要函数作为多个与单个设备对象相关联的子设备的容器。 总线驱动程序创建单个*物理设备对象 (PDO)* 它们枚举每个插即用 (PnP) 节点。

对于音频的适配器，单个的即插即用节点通常包含多个音频函数。 若要公开与节点关联作为不同的设备通常的各种函数，需要编写适配器总线驱动程序。 总线驱动程序枚举的硬件功能，并创建相应 PDOs。 在此方案中，一个或多个函数特定于驱动程序需要将绑定到 PDOs，再在适配器上的共享资源的访问权限的总线驱动程序与协商。

端口类驱动程序使用内核流式处理驱动程序的功能，操作系统会将设备识别为一组不同的子设备公开的单个设备对象的各个方面。

引用字符串追加到设备名称以指定所需的子。 内核流式处理驱动程序将 Irp 基于此引用字符串创建调度。 创建文件对象后，流式处理驱动程序内核提供的针对该文件对象，表示子的 Irp 调度。 此外，在端口类驱动程序实现基于 COM 的包装子设备模式。

适配器驱动程序实例化端口驱动程序和一个微型端口驱动程序并将其绑定的指针作为端口驱动程序的初始化函数的参数传递给微型端口驱动程序在一起 (请参阅中的代码示例[子创建](subdevice-creation.md)). 生成的端口/微型端口驱动程序堆栈构成表示端口类驱动程序支持的子类型之一的 KS 筛选器。

端口类驱动程序[ **PcRegisterSubdevice** ](https://msdn.microsoft.com/library/windows/hardware/ff537731)函数注册子，通过系统的其余部分被视为一种设备。 端口驱动程序接收 Irp 目标设备对象，但仅在其下注册的子字符串由指定这些 Irp 的创建。 端口驱动程序还会收到针对子与相关联的文件对象 Irp。 端口驱动程序是负责 KS 筛选器的子行为并相应地与微型端口驱动程序进行通信。

有关设计的多功能音频卡的驱动程序的详细信息，请参阅[多功能音频设备](multifunction-audio-devices.md)。

 

 




