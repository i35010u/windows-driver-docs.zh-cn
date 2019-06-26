---
Description: 描述 USB 类型 C 端口控制器接口类扩展，称为 UcmTcpciCx 和客户端驱动程序必须为 USB 类型 C 端口控制器执行的任务的行为。
title: 编写 USB 类型 C 端口控制器驱动程序
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: f2fcf5bef8d68b00ed78fcebfe858372d7425821
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385347"
---
# <a name="write-a-usb-type-c-port-controller-driver"></a>编写 USB 类型 C 端口控制器驱动程序

您需要编写 USB 类型 C 端口控制器驱动程序，如果您的 USB 类型 C 硬件实现 USB 类型-C 或 Power 传递 (PD) 物理层，但不实现所需的功率输出的状态机。 

Windows 10，版本 1703，USB 类型 C 体系结构进行了改进以支持硬件设计实现 USB 类型-C 或 Power 传递 (PD) 物理层，但不具有相应 PD 策略引擎或协议层实现。 对于这些设计，Windows 10 1703年版提供了基于软件的 PD 策略引擎和设备策略管理器通过名为"USB 连接器管理器类型 C 端口控制器接口类扩展"(UcmTcpciCx) 的新类扩展。 由 IHV 或 OEM/考虑了 ODM 编写的客户端驱动程序与 UcmTcpciCx 以提供有关硬件事件 PD 策略引擎和设备策略管理器中 UcmTcpciCx 函数所需的信息进行通信。 通过一组编程接口，本主题中以及参考部分中所述启用此通信。

![usb 连接器管理器](images/tcpci-arch.png)

UcmTcpciCx 类扩展本身就是 UcmCx 的客户端驱动程序。 有关 power 协定，数据角色的策略决策是在 UcmCx 中进行，并转发到 UcmTcpciCx。 UcmTcpciCx 实现这些策略，并使用 UcmTcpciCx 客户端驱动程序提供的端口控制器接口管理类型 C 和 PD 状态机。 


**摘要**
- 提供的 UcmTcpci 类扩展服务
- 客户端驱动程序的预期的行为

**正式规范**
-   [USB 类型 C 端口控制器接口规范]
-   [USB 3.1 和 USB 类型 C 规范](https://go.microsoft.com/fwlink/p/?LinkId=699515)
-   [USB 供电](https://go.microsoft.com/fwlink/p/?LinkID=623310)

适用于：

- Windows 10

**WDF 版本**

-   KMDF 版本 1.15

**上次更新时间：**

-   2017 年 5 月

**重要的 API**

[USB 类型 C 端口控制器界面驱动程序类扩展参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#type-c-driver-reference)

**UcmTcpciCx 客户端驱动程序模板**

[UcmTcpciCx 客户端驱动程序模板](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmTcpciCxClientSample)

## <a name="before-you-begin"></a>开始之前...

-   确定驱动程序需要编写具体取决于你的硬件或固件是否实现 PD 状态机类型。 有关详细信息，请参阅[USB 类型 C 连接器的开发 Windows 驱动程序](developing-windows-drivers-for-usb-type-c-connectors.md)。  

-   Windows 10 桌面版本安装 （主页、 专业版、 企业版和教育） 在目标计算机或 Windows 10 移动版上使用 USB 类型 C 连接器。
-   [安装](https://go.microsoft.com/fwlink/p/?LinkID=845980)最新 Windows 驱动程序工具包 (WDK) 在开发计算机上。 该工具包具有必需的标头文件和库，用于编写客户端驱动程序，具体而言，你将需要：

    -   存根 （stub） 库中，(UcmTcpciCxStub.lib)。 库将转换所做的客户端驱动程序的调用，并将其传递到此类扩展。
    -   标头文件，UcmTcpciCx.h。

    客户端驱动程序在内核模式下运行，并将绑定到 KMDF 1.15 库。 

    ![ucm 的 visual studio 配置](images/ucmtcpci-vs.png)

-  确定客户端驱动程序是否支持警报。

- 端口控制器不需要为 TCPCI 合规。 该接口捕获的任何类型 C 端口控制器的功能。 只需编写不 TCPCI 符合标准的硬件的 UcmTcpciCx 客户端驱动程序包括映射到硬件的寄存器和 TCPCI 规范中的命令的含义。 

- 大多数 TCPCI 控制器都是我<sup>2</sup>C 连接。 客户端驱动程序将使用串行外围总线 （存储） 连接资源和中断行与硬件进行通信。 该驱动程序将使用存储框架扩展 (SpbCx) 编程接口。 熟悉 SpbCx 通过阅读这些主题：
    - [简单外围总线 （存储） 驱动程序设计指南]
    - [编程参考的存储驱动程序] 

-   了解使用 Windows Driver Foundation (WDF)。 推荐阅读的主题：[使用 Windows Driver Foundation 开发驱动程序]( https://go.microsoft.com/fwlink/p/?LinkId=691676)、 由 Penny Orwick 和 Smith 专家编写。

## <a name="behavior-of-the-ucmtcpci-class-extension"></a>UcmTcpci 类扩展的行为

 -  作为状态机执行的一部分，UcmTcpciCx 将 IOCTL 请求发送到端口控制器。 例如，在消息传送中 PD，它发送 IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_TRANSMIT_BUFFER 请求以设置传输缓冲区。 该请求 (TRANSMIT_BUFFER) 移交给客户端驱动程序。 该驱动程序然后将缓冲区设置为传输提供的类扩展的详细信息。 

-   UcmTcpciCx 实现有关 power 协定、 数据角色等的策略。  


## <a name="expected-behavior-of-the-client-driver"></a>客户端驱动程序的预期的行为

应为 UcmTcpciCx 客户端驱动程序：

-   为电源策略所有者。 UcmTcpciCx 不参与端口控制器的电源管理。 

-   转换从 UcmTcpciCx，接收的请求到硬件读取或写入命令。 命令必须是异步的因为 DPM 不能阻止等待硬件传输完成。  

-   提供一个包含框架的请求对象的 framework 队列对象。 对于每个请求 UcmTcpci 类扩展想要将发送到客户端驱动程序，通过扩展驱动程序的队列对象中添加请求对象。 完成该驱动程序处理请求，调用 WdfRequestComplete。 它是客户端驱动程序的责任及时完成请求。 

-   发现和报告端口控制器的功能。 这些功能包括如端口控制器可以在运行的角色的信息 (如源只、 仅接收器 DRP)。 但是，还有其他一些功能的连接器 （请参阅有关功能存储区的说明） 和作为一个整体，DPM 所需知道，才能正确实现的 USB 类型 C 和 PD 策略的系统。 例如，DPM 需要知道要播发到端口合作伙伴系统/连接器的源功能。 

    **请注意功能存储区** 
        
    除了客户端驱动程序相关功能以外的其他信息来自系统全局位置称为_功能存储区_。 此系统全局功能存储区存储在 ACPI。 它是静态系统的功能和每个 DPM 使用来确定策略以实现其 USB 类型 C 连接器的说明。 
      
    通过从端口控制器的客户端驱动程序分离的系统功能的说明，设计使驱动程序的不同功能的不同系统上使用。 UcmCx，不 UcmTcpciCx，接口与功能存储区。 UcmTcpciCx （或其客户端驱动程序） 不与功能存储区交互。 
      
    如果适用，从功能存储区的信息将覆盖直接来自端口的控制器客户端驱动程序的信息。 例如，端口控制器仅限接收器的操作的支持，客户端驱动程序报告该信息。 但是，系统的其余部分可能未正确配置为仅限接收器的操作。 在这种情况下，系统制造商可以报告连接器是支持的功能存储区中的仅限于源的操作。 功能存储区，优先于驱动程序中的设置报告的信息。 

-   通知 UcmTcpciCx 包含与警报相关的所有相关数据。 
 
-   可选。 执行一些额外的处理的备用模式输入/退出。 该驱动程序通过 IOCTL 请求类扩展告知有关这些状态信息。 


## <a name="1-register-the-client-driver-with-ucmtcpcicx"></a>1.向 UcmTcpciCx 注册客户端驱动程序

示例引用：请参阅`EvtPrepareHardware`在`Device.cpp`。

1.  在 EVT_WDF_DRIVER_DEVICE_ADD 实现中，调用 UcmTcpciDeviceInitInitialize 初始化 WDFDEVICE_INIT 不透明结构。 调用将客户端驱动程序与框架相关联。

2.  创建框架设备对象 (WDFDEVICE) 后，调用 UcmTcpciDeviceInitialize UcmTcpciCx 注册客户端驱动程序。

## <a name="2-initialize-the-i2c-communications-channel-to-the-port-controller-hardware"></a>2.初始化到端口控制器硬件 I2C 通信通道。

示例引用：请参阅`EvtCreateDevice`在`Device.cpp`。

在 EVT_WDF_DEVICE_PREPARE_HARDWARE 实现中，读取的硬件资源，以打开通信通道。 这被必须检索 PD 功能并获取有关警报的通知。 

大多数 TCPCI 控制器都是我<sup>2</sup>C 连接。 在引用示例中，客户端驱动程序将打开我<sup>2</sup>通过使用存储框架扩展 (SpbCx) 编程接口的通道。 

客户端驱动程序通过调用 WdfCmResourceListGetDescriptor 枚举的硬件资源。 

为中断时收到警报。 因此，该驱动程序创建 framework 中断对象，并注册 ISR 将处理，将发出警报。  ISR 执行读取的硬件和硬件访问完成之前阻止写入操作。 由于等待在 DIRQL 不可接受，驱动程序将执行在 passive_level 调用 ISR。 


## <a name="3-initialize-the-port-controllers-type-c-and-pd-capabilities"></a>3.初始化端口控制器类型 C 和 PD 功能
    
示例引用：请参阅`EvtDeviceD0Entry`在`Device.cpp`。


 在 EVT_WDF_DEVICE_D0_EXIT 实现中， 
 
 1. 与端口控制器硬件进行通信并通过阅读各种寄存器中检索设备 identificaton 和功能。 
 
 2. 初始化 UCMTCPCI_PORT_CONTROLLER_IDENTIFICATION 和 UCMTCPCI_PORT_CONTROLLER_CAPABILITIES 与检索到的信息。 

 3. 通过将初始化的结构传递到 UCMTCPCI_PORT_CONTROLLER_CONFIG_INIT 初始化 UCMTCPCI_PORT_CONTROLLER_CONFIG 结构与上述信息。

 4. 调用 UcmTcpciPortControllerCreate 以创建端口控制器对象并检索 UCMTCPCIPORTCONTROLLER 句柄。

## <a name="4-set-up-a-framework-queue-object-for-receiving-requests-from-ucmtcpcicx"></a>4.设置用于接收请求从 UcmTcpciCx framework 队列对象

示例引用：请参阅`EvtDeviceD0Entry`中`Device.cpp`并`HardwareRequestQueueInitialize`中`Queue.cpp`。

 1. 在 EVT_WDF_DEVICE_D0_EXIT 实现中，通过调用 WdfIoQueueCreate 创建 framework 队列对象。 在该调用中，将需要注册回调实现来处理发送的 UcmTpciCx IOCTL 请求。 客户端驱动程序可能使用电源管理队列。 

    类型-C PD 状态机的执行，过程 UcmTpciCx 将命令发送到客户端驱动程序执行。 UcmTcpciCx 保证将会出现最多一个未完成端口控制器请求在任何给定时间。  
 
 2. 调用 UcmTcpciPortControllerSetHardwareRequestQueue UcmTpciCx 注册新的 framework 队列对象。 该调用成功后，UcmTcpciCx 将放置在此队列 framework 队列对象 (WDFREQUEST)，需要从驱动程序的操作时。 

 3. 实现 EvtIoDeviceControl 回调函数来处理这些 Ioctl。 

|  控制代码 |  描述 | 
|---            |           ---|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_GET_STATUS|   获取根据通用串行总线类型 C 端口控制器接口规范的所有状态寄存器的值。 客户端驱动程序必须检索 CC_STATUS、 POWER_STATUS 和 FAULT_STATUS 寄存器的值。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_GET_CONTROL|获取根据通用串行总线类型 C 端口控制器接口规范定义的所有控制寄存器的值。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_CONTROL|设置控制寄存器根据通用串行总线类型 C 端口控制器接口规范定义的值。| 
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_TRANSMIT|根据通用串行总线类型 C 端口控制器接口规范定义传输注册集。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_TRANSMIT_BUFFER|根据通用串行总线类型 C 端口控制器接口规范定义 TRANSMIT_BUFER 注册集。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_RECEIVE_DETECT|根据通用串行总线类型 C 端口控制器接口规范定义 RECEIVE_DETECT 注册集。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_CONFIG_STANDARD_OUTPUT|根据通用串行总线类型 C 端口控制器接口规范定义 CONFIG_STANDARD_OUTPUT 注册集。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_COMMAND|设置命令寄存器根据通用串行总线类型 C 端口控制器接口规范定义的值。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_MESSAGE_HEADER_INFO|根据通用串行总线类型 C 端口控制器接口规范定义集的 MESSAGE_HEADER_INFO 注册值。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_ALTERNATE_MODE_ENTERED|通知客户端驱动程序，以便该驱动程序可以执行其他任务输入备用模式。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_ALTERNATE_MODE_EXITED|通知客户端驱动程序，以便该驱动程序可以执行其他任务退出备用模式。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_CONFIGURED|通知客户端驱动程序，合作伙伴设备上的 DisplayPort 备用模式已配置了固定分配，以便该驱动程序可以执行其他任务。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_HPD_STATUS_CHANGED|通知热插拔检测 DisplayPort 连接已更改，以便该驱动程序可以执行其他任务的状态的客户端驱动程序。|

4. 调用 UcmTcpciPortControllerStart 以指示 UcmTcpciCx 启动端口控制器。 UcmTcpciCx 假定 USB 类型 C 和功率输出的控制。 端口控制器启动后，UcmTcpciCx 可能会开始将请求放入硬件请求队列。 

 
## <a name="5-handlle-alerts-from-the-port-controller-hardware"></a>5.从端口控制器硬件 Handlle 警报

示例引用：请参阅`ProcessAndSendAlerts`在`Alert.cpp`。

客户端驱动程序必须处理警报 （或事件），它接收从端口控制器硬件，并将其发送到 UcmTcpciCx 与事件相关的数据。 

硬件警报发生时，警报将高固定端口控制器硬件驱动器。 这将导致客户端 （在步骤 2 中注册） 的驱动程序的 ISR 得以调用。 在例程服务在 passive_level 调用的硬件中断。 例程确定是否中断是端口控制器硬件; 发出的警报如果是这样，它完成警报的处理，并通过调用 UcmTcpciPortControllerAlert 通知 UcmTcpciCx。 

在调用之前 UcmTcpciPortControllerAlert，客户端负责包括 UCMTCPCI_PORT_CONTROLLER_ALERT_DATA 结构中的警报与相关的所有相关数据。 客户端提供了一系列，因为可能导致硬件无法同时添加多个警报处于活动状态的所有警报。 

下面是示例流任务与抄送状态报告更改。 

1. 客户端收到硬件警报。 

2. 客户端读取的警报的寄存器，并确定类型警报处于活动状态。 

3. 客户端读取 CC 状态注册，并介绍了在 UCMTCPCI_PORT_CONTROLLER_ALERT_DATA CC 状态寄存器的内容。 该驱动程序设置到 UcmTcpciPortControllerAlertCCStatus AlertType 成员和寄存器的 CCStatus 成员。

4. 客户端调用 UcmPortControllerAlert 发送数组硬件警报 UcmTcpciCx。 

5. 客户端清除警报 （这可能会随时发生后客户端检索警报信息） 

## <a name="6-process-requests-received-from-ucmtcpcicx"></a>6.从 UcmTcpciCx 收到的处理请求

示例引用：请参阅`PortControllerInterface.cpp`。

作为状态机执行的一部分，需要将请求发送到端口控制器 UcmTcpciCx。 例如，它需要设置 TRANSMIT_BUFFER。 此请求移交给客户端驱动程序。 驱动程序设置传输缓冲区与 UcmTcpciCx 所提供的详细信息。 大多数这些请求转换为硬件读取或写入客户端驱动程序。 命令必须是异步的因为 DPM 不能阻止等待硬件传输完成。

UcmTcpciCx 将命令发送 I/O 的控制代码作为描述从客户端驱动程序所需的 get/set 操作。 在客户端驱动程序的队列设置中，该驱动程序注册 UcmTcpciCx 其队列。  UcmTcpciCx 开始在队列中放置 framework 请求对象，它需要从驱动程序的操作。 步骤 4 中的表中列出了 I/O 控制代码。

负责在客户端驱动程序来完成及时的请求。

完成请求的操作时，客户端驱动程序对其完成状态的 framework 请求对象调用 WdfRequestComplete。 

客户端驱动程序可能需要将 I/O 请求发送到另一个驱动程序来执行硬件操作。 例如，在示例中，该驱动程序存储将请求发送到我<sup>2</sup>C 连接端口控制器。 在这种情况下，该驱动程序不能转发它来自 UcmTcpciCx 因为请求对象可能没有正确数目的堆栈位置中 WDM IRP 的 framework 请求对象。 客户端驱动程序必须创建另一个框架请求对象并将其转发到另一个驱动程序。 客户端驱动程序可以预分配其在初始化期间，而不是创建一个每次从 UcmTcpciCx 收到请求时所需的请求对象。 这可能是因为 UcmTcpciCx 有可确保只有一个请求未完成任何给定时间。 

## <a name="see-also"></a>请参阅
[USB 类型 C 端口控制器界面驱动程序类扩展参考](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt805826(v=vs.85))
