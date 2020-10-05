---
title: 蓝牙驱动程序堆栈
description: 蓝牙驱动程序堆栈
ms.assetid: fb13c300-f8ed-4d82-8625-79db4d7feac5
keywords:
- 蓝牙 WDK，驱动程序堆栈
- 驱动程序堆栈 WDK 蓝牙
- 堆积 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 464546133002dd88daea523b582b06c881bac2d0
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733445"
---
# <a name="bluetooth-driver-stack"></a>蓝牙驱动程序堆栈


蓝牙驱动程序堆栈包含 Microsoft 为蓝牙协议提供的支持的核心部分。 在此堆栈中，启用 Bluetooth 的设备可以彼此定位，并建立连接。 跨此类连接，设备可以通过不同的应用程序交换数据并相互交互。

下图显示了蓝牙驱动程序堆栈中的模块以及 Windows Vista 和更高版本中不包含的可能的自定义用户模式和内核模式驱动程序。 这些自定义驱动程序称为配置文件驱动程序。

![阐释蓝牙驱动程序堆栈的关系图](images/bluetooth-architecture.png)

-   **用户模式**
    -   **用户模式应用**程序-一种用户模式应用程序，它通过已发布的 Api 访问蓝牙驱动程序堆栈。 有关详细信息，请参阅关于 Windows SDK 文档中的 [蓝牙](/windows/win32/bluetooth/about-bluetooth) 。

        **注意**   用户模式应用程序应链接到*BthProps*（而不是*IrProps*），以便使用[**BluetoothSetLocalServiceInfo**](/windows/win32/api/bluetoothapis/nf-bluetoothapis-bluetoothsetlocalserviceinfo)等 api。

         

-   **配置文件驱动程序的示例**
    -   **Wap 内核模式驱动程序**- (WAP) 组件的无线应用程序协议是配置文件驱动程序的一个示例，它在 Windows 网络堆栈和 BthPort 之间进行通信，同时访问 L2CAP 接口和 L2CAP 中包含的 SDP 接口。 其他可能的配置文件包括高级音频分发配置文件 (A2DP) 、A/V 远程控制配置文件 (AVRCP) 、泛型 A/V 分布配置文件 (GAVDP) 和常见 ISDN 访问 (CIP) 配置文件。
    -   **音频内核模式驱动程序**-配置文件驱动程序的一个示例，它在 Windows 音频堆栈与 BthPort 之间进行通信，并访问后者中包含的 SCO 接口。 可能的配置文件包括免提免费配置文件 (HFP) ，耳机配置文件 (HSP) ，无线电话服务配置文件 (CTP) 和对讲机配置文件 (ICP) 。
        **注意**   Windows 8 开头的 Windows 中包含此配置文件驱动程序。

         

    -   **蓝牙 Le 核心速率监视器配置文件**-一个蓝牙 LE 配置文件驱动程序的示例，该驱动程序与蓝牙低能耗 (LE) API 通信。
-   **蓝牙驱动程序堆栈组件**
    -   **IrProps**-一个组件，用于对为第一个版本的蓝牙驱动程序堆栈创建的配置文件驱动程序的向后兼容。

        **请注意**，提供  **IrProps**只是为了向后兼容。 使用 **BthProps** 组件进行新的开发。

         

    -   **BthProps**-一个组件，其中包含蓝牙用户界面的实现，以及用户模式应用程序访问的蓝牙 api 的实现。 此组件通过 (RPC) 的远程过程调用将查询发送到 BthServ。 此外，BthProps 通过 private IOCTLs 通过 BthPort 执行 pin 交换。 请注意，BthProps 在具有启用蓝牙功能的收音机的任何系统上运行。
    -   **BthServ**-负责将查询数据缓存并转发到 Bthport 的服务。
    -   **BthCi**-蓝牙类安装程序。
    -   **WshBth**-蓝牙 Windows 套接 helper 组件。 Windows 套接字层调用 WshBth 来执行套接字操作。 WshBth 主要通过 TDI 接口调入 RfComm。 WshBth 还会调用 BthServ 来执行远程设备查询，并调用 BthPort 来执行本地广播查询。
    -   **FSquirt**-A Nonextensible 对象 EXCHANGE (OBEX) 组件允许用户通过开放式蓝牙连接发送和接收文件。 OBEX 通过 RFCOMM 使用 WshBth 组件与远程设备通信。
    -   **BthPrint**-一个组件，用于实现 (HCRP) 的硬拷贝电缆替换配置文件。 此组件允许打印系统向启用 Bluetooth 的打印机发送数据并接收数据。 BthPrint 与 BthPort 中的 SDP 接口进行通信，以查询远程打印机和 BthPort 中的 L2CAP 接口来发送和接收数据。
    -   **HidBth**-用于实现人体学接口设备 (HID) 配置文件的组件。 HidBth 还会与 BthPort 中的 L2CAP 和 SDP 接口通信。 HidBth 连接到 HID 堆栈非常类似于 USB HID 模块。
    -   **BthPan**-实现个人区域网 (平移) 配置文件的组件，提供跨开放式蓝牙连接的 TCP 连接。 在 Windows Vista 和 Windows XP 中，BthPan 仅支持传出连接。 BthPan 也是 BthPort 组件的客户端，并同时使用 L2CAP 和 SDP 接口。
    -   **RfComm**-用于实现蓝牙串行电缆仿真协议的组件。 RfComm 还使用 BthPort 中找到的 L2CAP 和 SDP 接口。 RfComm 的上边缘公开了 TDI 接口，允许此组件显示为网络传输。 这是 WshBth 连接到蓝牙以发送和接收来自用户模式 Api 的数据的方式。

        用户模式应用程序可使用 Windows SDK 中所述的 Winsock 接口访问 RfComm。

    -   **BthModem**-用于实现虚拟 COM 端口和拨号网络的组件 (DUN) 。 BthModem 通过 TDI 接口将所有 i/o 和控制操作定向到 RfComm。 BthModem 的上部边缘与 *Serial.sys* 通信，使成为无线 COM 端口的外观。
        **注意**   此组件在 Windows RT 中不可用。

         

    -   **BthEnum**-蓝牙总线驱动程序。 BthEnum 与即插即用 (PnP) 管理器通信，以创建和销毁用于启用蓝牙服务的设备对象。 BthEnum 为连接的远程设备支持的每个服务创建一个 PDO。 例如，当用户连接支持蓝牙的鼠标时，Windows 将发现鼠标支持蓝牙 HID 服务，并为导致 PnP 管理器加载 HidBth 的 HID 服务创建一个 PDO。

        **注意**   对于*Bth*中指定的**UnsupportedServices**注册表项中显示的服务，BthEnum 将不会创建 PDOs。

         

    -   **BthLEEnum**-蓝牙低能耗 (LE) 总线驱动程序。 BthLEEnum 实现 ATT 协议和 GATT 配置文件。 它还负责创建 PDOs 来表示远程设备及其主服务。

    -   **BthPort**-BthUsb 微型端口加载的微型驱动程序。 BthPort 提供了四个组件：
        -   HCI 组件通过主机控制器接口与蓝牙规范中定义 (HCI) 的本地支持蓝牙的无线电通信。 由于所有启用 Bluetooth 的无线电设备都实现了 HCI 规范，因此 BthPort 能够与任何启用 Bluetooth 的无线电通信，而不管制造商或型号如何。
        -   SCO 组件实现面向同步连接的 (SCO) 协议。 此协议支持创建到远程设备的点到点连接。 SCO 客户端通过 [构建并发送](building-and-sending-a-brb.md) 蓝牙请求块 (BRBs) 与 SCO 接口通信。
        -   L2CAP 实现蓝牙逻辑链接控制和适配协议。 此协议支持将无损通道创建到远程设备。 L2CAP 客户端通过构建并发送蓝牙请求块 (BRBs) 来与 L2CAP 接口通信。
        -   SDP 实现蓝牙服务发现协议。
    -   **BthUsb.sys**-从 **BthPort**抽象总线接口的微型端口。

