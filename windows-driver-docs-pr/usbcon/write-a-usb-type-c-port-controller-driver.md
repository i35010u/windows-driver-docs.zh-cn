---
description: '描述 USB C # # 端口控制器接口类扩展的行为（称为 UcmTcpciCx），以及客户端驱动程序必须为 USB 类型 C 端口控制器执行的任务。'
title: 编写 USB 类型 C 端口控制器驱动程序
ms.date: 01/07/2019
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 5103b15a5e38d6474852bdf66f15b08882c03e9f
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968842"
---
# <a name="write-a-usb-type-c-port-controller-driver"></a>编写 USB 类型 C 端口控制器驱动程序

如果 USB C # c # 硬件实现 USB 类型 C 或电源传递 (PD) 物理层，但不实现电源交付所需的状态机，则需要写入 USB 类型 C 端口控制器驱动程序。 

在 Windows 10 （版本1703）中，USB 类型 C 体系结构经过了改进，可支持实现 USB 类型 C 或电源交付 (PD) 物理层，但没有相应的 PD 策略引擎或协议层实现的硬件设计。 对于这些设计，Windows 10 版本1703通过一个名为 "USB 连接器管理器 C # C # Class Extension" (UcmTcpciCx) 的新类扩展，提供基于软件的 PD 策略引擎和设备策略管理器。 由 IHV 或 OEM/ODM 编写的客户端驱动程序与 UcmTcpciCx 通信，以提供有关 PD 策略引擎和 UcmTcpciCx 中的设备策略管理器所需的硬件事件的信息。 通过本主题中所述的一组编程接口和参考部分来实现该通信。

![usb 连接器管理器](images/tcpci-arch.png)

UcmTcpciCx 类扩展本身就是 UcmCx 的客户端驱动程序。 有关电源协定、数据角色的策略决策在 UcmCx 中进行，并转发到 UcmTcpciCx。 UcmTcpciCx 实现了这些策略，并使用 UcmTcpciCx 客户端驱动程序提供的端口控制器接口管理类型 C 和 PD 状态机。 


**摘要**
- UcmTcpci 类扩展提供的服务
- 客户端驱动程序的预期行为

**官方规范**
-   [USB 类型-C 端口控制器接口规格]
-   [USB 3.1 和 USB 类型-C 规范](https://go.microsoft.com/fwlink/p/?LinkId=699515)
-   [USB 电源交付](https://go.microsoft.com/fwlink/p/?LinkID=623310)

适用于：

- Windows 10

**WDF 版本**

-   KMDF 版本1.15

**上次更新时间：**

-   2017 年 5 月

**重要的 API**

[USB 类型 C 端口控制器接口驱动程序类扩展参考](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#type-c-driver-reference)

**UcmTcpciCx 客户端驱动程序模板**

[UcmTcpciCx 客户端驱动程序模板](https://github.com/Microsoft/Windows-driver-samples/tree/master/usb/UcmTcpciCxClientSample)

## <a name="before-you-begin"></a>开始之前 .。。

-   确定需要写入的驱动程序类型，具体取决于你的硬件或固件是否实现了 PD 状态机。 有关详细信息，请参阅 [开发适用于 USB 类型 C 连接器的 Windows 驱动程序](developing-windows-drivers-for-usb-type-c-connectors.md)。  

-   在目标计算机上安装适用于桌面版的 Windows 10，并使用 USB 类型 C 连接器安装 Windows 10 移动版)  (。
-   在开发计算机上 (WDK) [安装](https://go.microsoft.com/fwlink/p/?LinkID=845980)最新的 Windows 驱动程序工具包。 工具包具有写入客户端驱动程序所需的头文件和库，具体而言，你将需要：

    -   存根库， (UcmTcpciCxStub) 。 库转换客户端驱动程序发出的调用，并将其传递给类扩展。
    -   标头文件 UcmTcpciCx。

    客户端驱动程序在内核模式下运行并绑定到 KMDF 1.15 库。 

    ![适用于 ucm 的 visual studio 配置](images/ucmtcpci-vs.png)

-  确定客户端驱动程序是否将支持警报。

- 你的端口控制器不需要与 TCPCI 兼容。 接口捕获任何类型 C 端口控制器的功能。 为不符合 TCPCI 的硬件编写 UcmTcpciCx 客户端驱动程序只需将 TCPCI 规范中的寄存器和命令的含义映射到硬件的含义即可。 

- 大多数 TCPCI 控制器都是 I<sup>2</sup>C 连接的。 你的客户端驱动程序将使用串行外围总线 (SPB) 连接资源和中断线路来与硬件通信。 驱动程序将使用 SPB 框架扩展 (SpbCx) 编程 intefaces。 阅读以下主题，熟悉 SpbCx：
    - [简单外围总线 (SPB) 驱动程序设计指南]
    - [SPB 驱动程序编程参考] 

-   熟悉 Windows Driver Foundation (WDF) 。 建议读物： [开发带有 Windows Driver Foundation 的驱动程序]( https://go.microsoft.com/fwlink/p/?LinkId=691676)（由 "Orwick" 和 "专家 Smith" 编写）。

## <a name="behavior-of-the-ucmtcpci-class-extension"></a>UcmTcpci 类扩展的行为

 -  在状态机执行过程中，UcmTcpciCx 会将 IOCTL 请求发送到端口控制器。 例如，在 PD 消息传递中，它发送 IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_TRANSMIT_BUFFER 请求来设置传输缓冲区。 该请求 (TRANSMIT_BUFFER) 将移交给客户端驱动程序。 然后，该驱动程序使用类扩展提供的详细信息设置传输缓冲区。 

-   UcmTcpciCx 实现有关电源协定、数据角色等的策略。  


## <a name="expected-behavior-of-the-client-driver"></a>客户端驱动程序的预期行为

UcmTcpciCx 的客户端驱动程序应为：

-   成为电源策略所有者。 UcmTcpciCx 不参与端口控制器的电源管理。 

-   将从 UcmTcpciCx 接收的请求转换为硬件读取或写入命令。 命令必须是异步的，因为 DPM 无法阻止等待硬件传输完成。  

-   提供包含框架请求对象的框架队列对象。 对于 UcmTcpci 类扩展要发送到客户端驱动程序的每个请求，该扩展在驱动程序的 queue 对象中添加了一个 request 对象。 当驱动程序处理完请求后，它将调用 WdfRequestComplete。 客户端驱动程序负责及时完成请求。 

-   发现和报告端口控制器的功能。 这些功能包括诸如端口控制器可以在 (（例如仅限源、仅限接收器、DRP) ）操作的角色等信息。 但是，连接器的其他功能 (参阅有关功能存储) 的说明，以及整个系统的相关说明，DPM 需要知道才能正确实现 USB 类型 C 和 PD 策略。 例如，DPM 需要知道系统/连接器的源功能才能将其播发到端口伙伴。 

    **便笺功能存储** 
        
    除了与客户端驱动程序相关的功能之外，其他信息来自称为 " _功能存储_" 的系统全局位置。 此系统全局功能存储存储在 ACPI 中。 它是系统功能的静态说明，DPM 用来确定要实现的策略的每个 USB 类型 C 连接器。 
      
    通过从端口控制器的客户端驱动程序中分离系统功能的说明 () ，该设计允许在不同功能的不同系统上使用驱动程序。 UcmCx （而非 UcmTcpciCx）与功能存储区的接口。 UcmTcpciCx (或它的客户端驱动程序) 不与功能存储区交互。 
      
    在适用的情况下，来自功能存储区的信息将覆盖直接来自端口控制器客户端驱动程序的信息。 例如，端口控制器支持仅接收操作，客户端驱动程序将报告该信息。 但是，对于仅接收操作，系统的其余部分可能没有正确配置。 在这种情况下，系统制造商可以报告连接器是否能够在功能存储中进行仅源操作。 功能存储中的设置优先于驱动程序报告的信息。 

-   向 UcmTcpciCx 通知与警报相关的所有相关数据。 
 
-   可选。 输入/退出备用模式后，执行一些额外的处理。 类扩展通过 IOCTL 请求通知驱动程序有关这些状态的信息。 


## <a name="1-register-the-client-driver-with-ucmtcpcicx"></a>1. 将客户端驱动程序注册到 UcmTcpciCx

示例参考：请参阅 `EvtPrepareHardware` 中的 `Device.cpp` 。

1.  在 EVT_WDF_DRIVER_DEVICE_ADD 实现中，调用 UcmTcpciDeviceInitInitialize 以初始化 WDFDEVICE_INIT 的不透明结构。 调用将客户端驱动程序与框架相关联。

2.  创建框架设备对象 (WDFDEVICE) 后，调用 UcmTcpciDeviceInitialize 将客户端驱动程序注册到 UcmTcpciCx。

## <a name="2-initialize-the-i2c-communications-channel-to-the-port-controller-hardware"></a>2. 将 I2C 通信通道初始化为端口控制器硬件。

示例参考：请参阅 `EvtCreateDevice` 中的 `Device.cpp` 。

在 EVT_WDF_DEVICE_PREPARE_HARDWARE 实现中，读取硬件资源以打开信道。 这是检索 PD 功能并获取有关警报的通知所必需的。 

大多数 TCPCI 控制器都是 I<sup>2</sup>C 连接的。 在参考示例中，客户端驱动程序使用 SPB 框架扩展打开 I<sup>2</sup> 通道， (SpbCx) 编程 intefaces。 

客户端驱动程序通过调用 WdfCmResourceListGetDescriptor 来枚举硬件资源。 

警报作为中断接收。 因此，驱动程序将创建一个框架中断对象，并注册将处理警报的 ISR。  ISR 执行硬件读写操作，这些操作会一直阻止到完成硬件访问。 由于等待在 DIRQL 上是不可接受的，因此驱动程序会在 PASSIVE_LEVEL 执行 ISR。 


## <a name="3-initialize-the-port-controllers-type-c-and-pd-capabilities"></a>3. 初始化端口控制器的类型 C 和 PD 功能
    
示例参考：请参阅 `EvtDeviceD0Entry` 中的 `Device.cpp` 。


 在 EVT_WDF_DEVICE_D0_EXIT 实现中， 
 
 1. 通过读取各种寄存器与端口控制器硬件通信并检索设备 identificaton 和功能。 
 
 2. 用检索到的信息初始化 UCMTCPCI_PORT_CONTROLLER_IDENTIFICATION 和 UCMTCPCI_PORT_CONTROLLER_CAPABILITIES。 

 3. 通过将初始化的结构传递到 UCMTCPCI_PORT_CONTROLLER_CONFIG_INIT，用前面的信息初始化 UCMTCPCI_PORT_CONTROLLER_CONFIG 结构。

 4. 调用 UcmTcpciPortControllerCreate 创建端口控制器对象并检索 UCMTCPCIPORTCONTROLLER 句柄。

## <a name="4-set-up-a-framework-queue-object-for-receiving-requests-from-ucmtcpcicx"></a>4. 设置一个框架队列对象用于接收来自 UcmTcpciCx 的请求

示例参考： `EvtDeviceD0Entry` 在 `Device.cpp` 和中 `HardwareRequestQueueInitialize` 查看 `Queue.cpp` 。

 1. 在 EVT_WDF_DEVICE_D0_EXIT 实现中，通过调用 WdfIoQueueCreate 来创建框架队列对象。 在该调用中，你将需要注册回调实现以处理 UcmTpciCx 发送的 IOCTL 请求。 客户端驱动程序可以使用电源管理的队列。 

    在类型 C 和 PD 状态机的执行过程中，UcmTpciCx 向客户端驱动程序发送要执行的命令。 UcmTcpciCx 保证在任何给定时间最多有一个未完成的端口控制器请求。  
 
 2. 调用 UcmTcpciPortControllerSetHardwareRequestQueue，将新的框架队列对象注册到 UcmTpciCx。 该调用成功后，UcmTcpciCx 会将框架队列对象 (在此队列中) ，因为它需要驱动程序的操作。 

 3. 实现 EvtIoDeviceControl 回调函数来处理这些 IOCTLs。 

|  控制代码 |  说明 | 
|---            |           ---|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_GET_STATUS|   按通用串行总线类型 C 端口控制器接口规范获取所有状态寄存器的值。 客户端驱动程序必须检索 CC_STATUS、POWER_STATUS 和 FAULT_STATUS 寄存器的值。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_GET_CONTROL|获取根据通用串行总线类型 C 端口控制器接口规范定义的所有控制寄存器的值。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_CONTROL|根据通用串行总线类型 C 端口控制器接口规范设置定义的控制寄存器的值。| 
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_TRANSMIT|设置按通用串行总线类型 C 端口控制器接口规范定义的传输寄存器。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_TRANSMIT_BUFFER|根据通用串行总线类型 C 端口控制器接口规范设置定义的 TRANSMIT_BUFER Register。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_RECEIVE_DETECT|根据通用串行总线类型 C 端口控制器接口规范设置定义的 RECEIVE_DETECT Register。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_CONFIG_STANDARD_OUTPUT|根据通用串行总线类型 C 端口控制器接口规范设置定义的 CONFIG_STANDARD_OUTPUT Register。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_COMMAND|设置根据通用串行总线类型 C 端口控制器接口规范定义的命令寄存器的值。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_SET_MESSAGE_HEADER_INFO|根据通用串行总线类型 C 端口控制器接口规范设置定义的 MESSAGE_HEADER_INFO 寄存器的值。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_ALTERNATE_MODE_ENTERED|通知客户端驱动程序已进入备用模式，以便驱动程序可以执行其他任务。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_ALTERNATE_MODE_EXITED|通知客户端驱动程序已退出备用模式，以便驱动程序可以执行其他任务。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_CONFIGURED|通知客户端驱动程序：伙伴设备上的 DisplayPort 备用模式已配置了 pin 分配，以便驱动程序可以执行其他任务。|
|IOCTL_UCMTCPCI_PORT_CONTROLLER_DISPLAYPORT_HPD_STATUS_CHANGED|通知客户端驱动程序 DisplayPort 连接的热插拔检测状态已更改，以便驱动程序可以执行其他任务。|

4. 调用 UcmTcpciPortControllerStart 以指示 UcmTcpciCx 启动端口控制器。 UcmTcpciCx 假定控制 USB 类型 C 和电源。 端口控制器启动后，UcmTcpciCx 可能开始将请求放入硬件请求队列。 

 
## <a name="5-handle-alerts-from-the-port-controller-hardware"></a>5. 处理来自端口控制器硬件的警报

示例参考：请参阅 `ProcessAndSendAlerts` 中的 `Alert.cpp` 。

客户端驱动程序必须处理) 从端口控制器硬件接收到 (或事件的警报，并将它们发送到带有与事件相关的数据的 UcmTcpciCx。 

发生硬件警报时，端口控制器硬件会驱动警报引脚的高。 这会导致在第2步中注册的客户端驱动程序的 ISR () 调用。 例程在 PASSIVE_LEVEL 的硬件中断。 例程确定中断是否是来自端口控制器硬件的警报;如果是，它将完成警报的处理，并通过调用 UcmTcpciPortControllerAlert 通知 UcmTcpciCx。 

在调用 UcmTcpciPortControllerAlert 之前，客户端负责在 UCMTCPCI_PORT_CONTROLLER_ALERT_DATA 结构中包含与警报相关的所有相关数据。 客户端提供所有处于活动状态的警报的数组，因为硬件可能会同时声明多个警报。 

下面是用于报告 CC 状态更改的任务示例。 

1. 客户端收到硬件警报。 

2. 客户端读取警报注册并确定活动的类型警报。 

3. 客户端读取 CC 状态寄存器，并描述 UCMTCPCI_PORT_CONTROLLER_ALERT_DATA 中 CC 状态寄存器的内容。 驱动程序将 AlertType 成员设置为 register 的 UcmTcpciPortControllerAlertCCStatus 和 CCStatus 成员。

4. 客户端调用 UcmPortControllerAlert 将阵列硬件警报发送到 UcmTcpciCx。 

5. 客户端会清除警报， (客户端检索警报信息后可能会发生这种情况)  

## <a name="6-process-requests-received-from-ucmtcpcicx"></a>6. 处理从 UcmTcpciCx 收到的请求

示例参考：请参阅 `PortControllerInterface.cpp` 。

在状态机执行过程中，UcmTcpciCx 需要向端口控制器发送请求。 例如，它需要设置 TRANSMIT_BUFFER。 此请求将移交给客户端驱动程序。 驱动程序使用 UcmTcpciCx 提供的详细信息设置传输缓冲区。 其中的大多数请求都转换为客户端驱动程序读取或写入的硬件。 命令必须是异步的，因为 DPM 无法阻止等待硬件传输完成。

UcmTcpciCx 将命令作为 i/o 控制代码发送，说明客户端驱动程序所需的 get/set 操作。 在客户端驱动程序的队列设置中，驱动程序将其队列注册到 UcmTcpciCx。  UcmTcpciCx 开始将框架请求对象放置在队列中，它需要驱动程序的操作。 在步骤4的表中列出了 i/o 控制代码。

客户端驱动程序负责及时完成请求。

在完成请求的操作后，客户端驱动程序将使用完成状态对框架请求对象调用 WdfRequestComplete。 

客户端驱动程序可能需要将 i/o 请求发送到另一个驱动程序，以执行硬件操作。 例如，在示例中，驱动程序将 SPB 请求发送到 I<sup>2</sup>C 连接端口控制器。 在这种情况下，驱动程序无法转发从 UcmTcpciCx 收到的框架请求对象，因为请求对象可能在 WDM IRP 中没有正确数目的堆栈位置。 客户端驱动程序必须创建另一个框架请求对象并将其转发给另一个驱动程序。 客户端驱动程序可以在初始化期间预分配它需要的请求对象，而无需在每次从 UcmTcpciCx 获取请求时创建一个对象。 这是可能的，因为 UcmTcpciCx 保证在任何给定时间都只有一个请求未完成。 

## <a name="see-also"></a>另请参阅
[USB 类型 C 端口控制器接口驱动程序类扩展参考](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/mt805826(v=vs.85))
