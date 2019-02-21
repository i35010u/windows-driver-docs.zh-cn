---
Description: Create a user-mode service that communicates with GenericUSBFn.sys by sending I/O control code (IOCTL) requests.
title: 从用户模式服务与 GenericUSBFn.sys 通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 638ad0ddee69f42aff323eb13195a744317214b5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544546"
---
# <a name="communicating-with-genericusbfnsys-from-a-user-mode-service"></a>从用户模式服务与 GenericUSBFn.sys 通信 


用户模式下的所有请求都发送到由 Microsoft 提供的内核模式驱动程序 GenericUSBFn.sys。 可以通过发送这些 I/O 控制代码 (IOCTL) 和 GenericUSBFn.sys 句柄与 USB 函数驱动程序的内核模式通信与 GenericUSBFn.sys 创建进行通信的用户模式服务。

在中声明 Ioctl [Genericusbfnioctl.h](https://docs.microsoft.com/windows/desktop/api/genericusbfnioctl/)用于与 GenericUSBFn.sys 从用户模式服务进行通信。


以下步骤介绍如何定义使用 GenericUSBFn.sys 要与其 USB 函数驱动程序进行交互的 USB 接口服务：

1. 在启动时，该服务侦听的接口的设备接口到达。 设备接口的 GUID 是 OEM 定义的 HKEY_LOCAL_MACHINE\CurrentControlSet\Control\USBFN\Interfaces 子项下的注册表中声明的 InterfaceGUID 值。 有两种设备到达所侦听的常用方法：
    - 触发器启动服务。 有关详细信息，请参阅服务触发器事件。 
    - 注册设备接口到达。 有关详细信息，请参阅 CM_Register_Notification 函数。 
2. 接口到达后，该服务将打开到设备的句柄： 
    - 通过调用 CM_Get_Device_Interface_List 函数获取设备的符号名称。 在注册表中的 InterfaceGUID 值中指定设备接口声明的 GUID。
    - 设备的符号名称后，请使用 CreateFile 打开到设备的句柄。 
3. 在注册表中配置时，该服务将颁发 IOCTL_GENERICUSBFN_GET_CLASS_INFO 来检索有关可用管道的信息。 
4. 服务已准备好进行通信后，它会发出 IOCTL_GENERICUSBFN_ACTIVATE_USB_BUS。 激活类的所有驱动程序后，USB 函数类扩展可以连接到主机。 
5. 若要接收 USB 通知，该服务将颁发 IOCTL_GENERICUSBFN_BUS_EVENT_NOTIFICATION。 此 IOCTL 完成新的 USB 事件发生时。 特定的感兴趣的事件 (USBFN_EVENT) 包括：
6. UsbfnEventReset:这用于确定连接的 USB 设备的速度。 
7. UsbfnEventConfigured:现在，服务可以发出传输请求。 
8. UsbfnEventSetupPacket:USB 函数类扩展已接收特定于接口的安装程序数据包 (bmRequestType.Type = = BMREQUEST_CLASS)。 服务应提供以下回复到安装程序的数据包通过发出传输请求管道 0，在握手请求 (IOCTL_GENERICUSBFN_CONTROL_STATUS_HANDSHAKE_OUT) 后跟管道 0 上的方向相反。 
9. 收到 UsbfnEventConfigured 事件后，该服务可以开始发出传输请求使用 IOCTL_GENERICUSBFN_TRANSFER_IN、 IOCTL_GENERICUSBFN_TRANSFER_IN_APPEND_ZERO_PKT 和 IOCTL_GENERICUSBFN_TRANSFER_OUT。 
