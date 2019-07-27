---
Description: 通过发送 i/o 控制代码 (IOCTL) 请求创建与 GenericUSBFn 通信的用户模式服务。
title: 从用户模式服务与 GenericUSBFn.sys 通信
ms.date: 07/26/2019
ms.localizationpriority: medium
ms.openlocfilehash: fa8b95867d129f49ad4abe4f294784eb77461dba
ms.sourcegitcommit: d7be945c4168756d5c11623b8ffb2880834d8382
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2019
ms.locfileid: "68590937"
---
# <a name="communicating-with-genericusbfnsys-from-a-user-mode-service"></a>从用户模式服务与 GenericUSBFn.sys 通信 


所有用户模式请求都将发送到 Microsoft 提供的内核模式驱动程序 GenericUSBFn。 可以通过发送这些 i/o 控制代码 (IOCTL) 来创建与 GenericUSBFn 通信的用户模式服务, 并使用 GenericUSBFn 处理与 USB 函数驱动程序的内核模式通信。

在[Genericusbfnioctl](https://docs.microsoft.com/windows/desktop/api/genericusbfnioctl/)中声明的 IOCTLs 用于从用户模式服务与 GenericUSBFn 进行通信。


以下步骤介绍如何定义与 GenericUSBFn 交互以与 USB function 驱动程序通信的 USB 接口服务:

1. 启动时, 该服务侦听接口的设备接口到达。 设备接口 GUID 是在 InterfaceGUID 中的 HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\USBFN\Interfaces. 的 OEM 定义子项下声明的值。 有两种方法可用于侦听设备到达:
    - 触发器启动该服务。 有关详细信息, 请参阅服务触发器事件。 
    - 注册以实现设备接口。 有关详细信息, 请参阅 CM_Register_Notification 函数。 
2. 接口到达后, 服务将打开设备的句柄: 
    - 通过调用 CM_Get_Device_Interface_List 函数获取设备的符号名称。 指定在注册表的 InterfaceGUID 值中声明的设备接口 GUID。
    - 获取设备的符号名称后, 通过使用 CreateFile 打开设备的句柄。 
3. 服务会发出 IOCTL_GENERICUSBFN_GET_CLASS_INFO 来检索有关在注册表中配置的可用管道的信息。 
4. 服务准备好进行通信后, 将发出 IOCTL_GENERICUSBFN_ACTIVATE_USB_BUS。 激活所有类驱动程序后, USB 函数类扩展可以连接到主机。 
5. 若要接收 USB 通知, 服务将发出 IOCTL_GENERICUSBFN_BUS_EVENT_NOTIFICATION。 此 IOCTL 在发生新的 USB 事件时完成。 特别感兴趣的事件 (USBFN_EVENT) 包括:
6. UsbfnEventReset:这用于确定连接的 USB 设备的速度。 
7. UsbfnEventConfigured:服务现在可以发出传输请求。 
8. UsbfnEventSetupPacket:USB 函数类扩展已接收接口特定的安装包 (bmRequestType = = BMREQUEST_CLASS)。 服务应通过在管道0中发出传输请求, 然后在管道0上反向反向握手请求 (IOCTL_GENERICUSBFN_CONTROL_STATUS_HANDSHAKE_OUT) 来回复安装包。 
9. 接收到 UsbfnEventConfigured 事件后, 服务可以使用 IOCTL_GENERICUSBFN_TRANSFER_IN、IOCTL_GENERICUSBFN_TRANSFER_IN_APPEND_ZERO_PKT 和 IOCTL_GENERICUSBFN_TRANSFER_OUT 开始发出传输请求。 
