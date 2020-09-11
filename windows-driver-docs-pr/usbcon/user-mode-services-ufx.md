---
description: 通过发送 i/o 控制代码 (IOCTL) 请求来创建与 GenericUSBFn.sys 通信的用户模式服务。
title: 从用户模式服务与 GenericUSBFn.sys 通信
ms.date: 07/26/2019
ms.localizationpriority: medium
ms.openlocfilehash: 1fe1133bb24170b9b8a3492664f12d4a3d6ba4df
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010491"
---
# <a name="communicating-with-genericusbfnsys-from-a-user-mode-service"></a>从用户模式服务与 GenericUSBFn.sys 通信 


所有用户模式请求都将发送到 Microsoft 提供的内核模式驱动程序 GenericUSBFn.sys。 可以通过将这些 i/o 控制代码发送 (IOCTL) ，并 GenericUSBFn.sys 处理与 USB 函数驱动程序的内核模式通信，来创建与 GenericUSBFn.sys 通信的用户模式服务。

在 [Genericusbfnioctl](/windows/desktop/api/genericusbfnioctl/) 中声明的 IOCTLs 用于与来自用户模式服务的 GenericUSBFn.sys 进行通信。


以下步骤描述了如何定义与 GenericUSBFn.sys 进行交互以与 USB 函数驱动程序通信的 USB 接口服务：

1. 启动时，该服务侦听接口的设备接口到达。 设备接口 GUID 是在 HKEY_LOCAL_MACHINE 注册表中的 InterfaceGUID 值中声明的值。 有两种方法可用于侦听设备到达：
    - 触发器启动该服务。 有关详细信息，请参阅服务触发器事件。 
    - 注册以实现设备接口。 有关详细信息，请参阅 CM_Register_Notification 函数。 
2. 接口到达后，服务将打开设备的句柄： 
    - 通过调用 CM_Get_Device_Interface_List 函数获取设备的符号名称。 指定在注册表的 InterfaceGUID 值中声明的设备接口 GUID。
    - 获取设备的符号名称后，通过使用 CreateFile 打开设备的句柄。 
3. 服务会发出 IOCTL_GENERICUSBFN_GET_CLASS_INFO 来检索有关在注册表中配置的可用管道的信息。 
4. 服务准备好进行通信后，会发出 IOCTL_GENERICUSBFN_ACTIVATE_USB_BUS。 激活所有类驱动程序后，USB 函数类扩展可以连接到主机。 
5. 若要接收 USB 通知，服务会发出 IOCTL_GENERICUSBFN_BUS_EVENT_NOTIFICATION。 此 IOCTL 在发生新的 USB 事件时完成。 特定兴趣 USBFN_EVENT) 事件 (包括：
6. UsbfnEventReset：用于确定连接的 USB 设备的速度。 
7. UsbfnEventConfigured：服务现在可以发出传输请求。 
8. UsbfnEventSetupPacket： USB 函数类扩展已收到特定于接口的安装数据包 (bmRequestType = = BMREQUEST_CLASS) 。 该服务应通过在管道0中发出传输请求来回复安装包，后跟握手请求 (IOCTL_GENERICUSBFN_CONTROL_STATUS_HANDSHAKE_OUT 在管道0上相反方向) 。 
9. 接收到 UsbfnEventConfigured 事件后，服务可以使用 IOCTL_GENERICUSBFN_TRANSFER_IN、IOCTL_GENERICUSBFN_TRANSFER_IN_APPEND_ZERO_PKT 和 IOCTL_GENERICUSBFN_TRANSFER_OUT 开始发出传输请求。