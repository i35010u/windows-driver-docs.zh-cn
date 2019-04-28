---
title: 蓝牙驱动程序堆栈
description: 蓝牙驱动程序堆栈
ms.assetid: fb13c300-f8ed-4d82-8625-79db4d7feac5
keywords:
- 蓝牙 WDK，驱动程序堆栈
- 驱动程序堆栈 WDK 蓝牙
- 堆栈 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c144d01f08e51cc218917c93b8dc6c8c5bc2d2f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63328321"
---
# <a name="bluetooth-driver-stack"></a>蓝牙驱动程序堆栈


蓝牙驱动程序堆栈包含由 Microsoft 提供的蓝牙协议支持的核心部分。 有了这个堆栈，启用了蓝牙的设备可以找到对方，并建立连接。 在此类连接，设备可以交换数据，并通过各种应用程序彼此之间交互。

下图显示了蓝牙驱动程序堆栈，以及可能的自定义用户模式和内核模式驱动程序未包含在 Windows Vista 及更高版本中的模块。 这些自定义驱动程序称为配置文件驱动程序。

![说明蓝牙驱动程序堆栈的关系图](images/bluetooth-architecture.png)

-   **User-mode**
    -   **用户模式应用程序**-通过已发布的 Api 访问蓝牙驱动程序堆栈的用户模式应用程序。 有关详细信息，请参阅[有关蓝牙](https://go.microsoft.com/fwlink/p/?linkid=50712)Windows SDK 文档中。

        **请注意**  用户模式应用程序应针对链接*BthProps.lib*，而不是*IrProps.lib*，以便使用 Api，如[ **BluetoothSetLocalServiceInfo**](https://msdn.microsoft.com/library/windows/hardware/ff536580)。

         

-   **配置文件驱动程序的示例**
    -   **WAP 内核模式驱动程序**-无线应用协议 (WAP) 组件是 Windows 网络堆栈和 BthPort，访问 L2CAP 接口和 SDP 接口 （可选） 之间进行通信的配置文件驱动程序的示例包含在 L2CAP 中。 其他可能的配置文件还包括高级音频分发配置文件 (A2DP) A / V 远程控制配置文件 (AVRCP) 泛型 A / V 分发配置文件 (GAVDP) 和常见 ISDN 访问 (CIP) 配置文件。
    -   **音频的内核模式驱动程序**-的 Windows 音频堆栈和 BthPort，访问包含在后者的 SCO 接口之间进行通信的配置文件驱动程序的示例。 可能的配置文件包括手可用配置文件 (HFP)、 耳机式配置文件 (HSP)、 无绳电话服务配置文件 (CTP) 和对讲机配置文件 (ICP)。
        **请注意**  此配置文件驱动程序随与 Windows 8 的 Windows 开始。

         

    -   **蓝牙 LE 心率监视器配置文件**-的通信使用蓝牙低能耗 (LE) API 的蓝牙 LE 配置文件驱动程序的示例。
-   **蓝牙驱动程序堆栈组件**
    -   **IrProps**-用于向后兼容性的第一个版本的蓝牙驱动程序堆栈创建的配置文件驱动程序的组件。

        **请注意**  **IrProps**仅为向后兼容性而提供。 使用**BthProps**组件进行新的开发。

         

    -   **BthProps**的一个组件，它包含实现的蓝牙用户接口实现的蓝牙 Api 以及该用户模式应用程序访问权限。 此组件将查询发送到 BthServ，通过远程过程调用 (RPC)。 此外，BthProps 执行与通过私有 Ioctl BthPort pin 交换。 请注意，BthProps 与已启用蓝牙的无线电收发器的任何系统上运行。
    -   **BthServ**-一种服务，负责缓存并转发到 Bthport 查询数据。
    -   **BthCi**-蓝牙类安装程序。
    -   **WshBth**-蓝牙 Windows 套接字帮助程序组件。 WshBth 由 Windows 套接字层来执行套接字操作调用。 WshBth 主要调用 RfComm 通过 TDI 接口。 WshBth 也会调用到 BthServ 执行远程设备的查询和 BthPort 执行本地无线电收发器的查询。
    -   **FSquirt**-使用户能够发送和接收文件打开蓝牙连接的 nonextensible 对象交换 (OBEX) 组件。 OBEX 与远程设备的整个 RFCOMM 使用 WshBth 组件进行通信。
    -   **BthPrint**-实现硬拷贝电缆替换配置文件 (HCRP) 的组件。 此组件允许将数据发送到和接收数据从启用 Bluetooth 的打印机的打印系统。 BthPrint 与 BthPort 查询远程打印机中的 SDP 接口并在 BthPort 发送和接收数据的 L2CAP 接口进行通信。
    -   **HidBth**-实现人体学接口设备 (HID) 配置文件的组件。 HidBth 还与中 BthPort L2CAP 和 SDP 接口通信。 HidBth 连接到 HID 堆栈更类似 USB HID 模块执行的操作。
    -   **BthPan**-实现个人区域网 (PAN) 配置文件中，打开蓝牙连接提供 TCP 连接的组件。 在 Windows Vista 和 Windows XP，BthPan 仅支持传出连接。 BthPan 也是 BthPort 组件的客户端，并使用 L2CAP 和 SDP 接口。
    -   **RfComm**-实现蓝牙串行电缆仿真协议的组件。 RfComm 还使用 BthPort 中找到的 L2CAP 和 SDP 接口。 RfComm 的上边缘显示 TDI 接口，从而使此组件以似乎是网络传输。 这是 WshBth 如何连接到 Bluetooth 发送和接收来自用户模式 Api 的数据。

        用户模式应用程序可以访问 RfComm 使用 Windows SDK 中所述的 Winsock 接口。

    -   **BthModem**-实现虚拟 COM 端口和拨号网络 (DUN) 的组件。 BthModem 指示所有 I/O 和控制操作到 RfComm 通过 TDI 接口。 BthModem 的上边缘与通信*Serial.sys*以提供进行无线的 COM 端口的外观。
        **请注意**  此组件不可用在 Windows rt。

         

    -   **BthEnum**-蓝牙总线驱动程序。 BthEnum 与插即用 (PnP) 管理器来创建和销毁设备对象用于启用蓝牙服务进行通信。 BthEnum 创建每个服务进行连接的远程设备支持 PDO。 例如，当用户已启用蓝牙的鼠标，Windows 将发现鼠标支持 HID 蓝牙服务并创建会导致 PnP 管理器中，以加载 HidBth 的 HID 服务 PDO。

        **请注意**  BthEnum 不会为出现在服务创建 PDOs **UnsupportedServices**注册表项中指定*Bth.inf*。

         

    -   **BthLEEnum**-蓝牙低能耗 (LE) 总线驱动程序。 BthLEEnum 实现 ATT 协议和 GATT 配置文件。 它也是负责创建 PDOs 来表示远程设备和其主服务。

    -   **BthPort**-微型驱动程序加载由 BthUsb 微型端口。 BthPort 提供了四个组件：
        -   HCI 组件进行通信的本地的已启用蓝牙的单选通过主机控制器接口 (HCI) 蓝牙规范中定义。 由于所有启用 Bluetooth 的无线收发器实现 HCI 规范，BthPort 是能够与任何已启用蓝牙的无线电收发器，而不考虑制造商或模型进行通信。
        -   SCO 组件实现 Synchronous Connection-Oriented (SCO) 协议。 此协议支持创建点到点连接到远程设备。 SCO 客户端与 SCO 接口的通信[生成和发送](building-and-sending-a-brb.md)蓝牙请求块 (BRBs)。
        -   L2CAP 实现蓝牙逻辑链接控件和适应协议。 此协议支持创建到远程设备的无损通道。 L2CAP 客户端与通信 L2CAP 接口通过生成并发送蓝牙请求块 (BRBs)。
        -   SDP 实现蓝牙服务发现协议。
    -   **BthUsb.sys**-将抽象化的总线接口的微型端口**BthPort**。

 

 





