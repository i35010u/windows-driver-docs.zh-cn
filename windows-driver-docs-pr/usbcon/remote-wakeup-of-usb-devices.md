---
Description: 本主题介绍有关在客户端驱动程序中实现远程唤醒功能的最佳做法。
title: 远程唤醒 USB 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ce455952b0b6b5dbf7624194a033c616ac0b90d9
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67358352"
---
# <a name="remote-wakeup-of-usb-devices"></a>远程唤醒 USB 设备


本主题介绍有关在客户端驱动程序中实现远程唤醒功能的最佳做法。

可以响应外部唤醒信号挂起时的 USB 设备被视为具有*远程唤醒*功能。 具有远程唤醒功能的设备的示例有鼠标、 键盘、 USB 集线器，调制解调器 （唤醒环），Nic，唤醒电缆插入。 所有这些设备都能够生成远程唤醒信号。 不能生成远程唤醒信号的设备包括视频摄像机、 大容量存储设备、 音频设备和打印机。

支持远程唤醒信号的设备驱动程序必须发出[ **IRP\_MN\_等待\_唤醒**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-wait-wake) IRP，也称为等待唤醒 IRP 到 arm 的设备远程唤醒。 等待唤醒机制部分所述[支持的设备是否已唤醒功能](https://docs.microsoft.com/windows-hardware/drivers/kernel/supporting-devices-that-have-wake-up-capabilities)。

## <a name="when-does-the-system-enable-remote-wakeup-on-a-usb-leaf-device"></a>系统何时启用 USB 叶设备上的远程唤醒？


在 USB 术语中，USB 设备可用于远程唤醒时其设备\_远程\_唤醒功能设置。 USB 规范指定主机软件必须设置"仅只是之前"将设备置于睡眠状态的设备上的远程唤醒功能。

出于此原因，USB 堆栈不会设置设备\_远程\_接收设备等待唤醒 IRP 后在设备上的唤醒功能。 相反，它会等到收到[ **IRP\_MN\_设置\_POWER** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-set-power)请求以更改到 D1/D2 WDM 设备状态的设备。 在大多数情况下，当 USB 堆栈收到此请求，它在设备上设置远程唤醒功能和方法让设备进入睡眠状态通过停用设备的上游端口。 在设计和调试您的驱动程序，应记住之间武装软件中唤醒的 USB 设备是松散关系，通过等待唤醒 IRP，和远程唤醒功能设置武装硬件中唤醒设备。

因为 D3 中的设备不能将系统唤醒 WDM 电源模型，根据接收请求，将设备更改为 D3，睡眠状态时，USB 堆栈不启用远程唤醒设备。

## <a name="why-does-attaching-or-detaching-my-device-produce-a-different-wakeup-behavior-in-windows-xp-and-windows-vista-and-later-versions-of-windows"></a>为什么连接或分离不同的唤醒行为在 Windows XP 和 Windows Vista 和更高版本的 Windows 中的设备产生？


WDM 电源模式的 USB 实现的另一个独特之处将远程唤醒的 USB 集线器的武装。 在 Microsoft Windows XP 中主控制器和 USB 设备之间的所有中心设备只要 USB 设备都有用于唤醒的唤醒都有。 这将产生令人惊讶的结果，处于睡眠状态的设备都分离时它们将唤醒系统。

在 Windows Vista 和更高版本的 Windows，如果总线上的 USB 叶设备有唤醒，USB 堆栈还 arm USB 主控制器唤醒，但它不一定将 arm 任何上游设备的 USB 集线器。 USB 集线器驱动程序武器远程唤醒 USB 堆栈配置为唤醒系统上才中心附加和分离 （即插即用/拔出） 事件。

**请注意**  UHCI （通用主机控制器接口） USB 主控制器，不要区分远程唤醒信号和连接根集线器端口上的更改事件。 这意味着系统将始终从较低的系统电源状态如果唤醒 USB 设备连接到或断开连接从根集线器端口，如果至少一个设备有 UHCI 控制器之后唤醒。

 

## <a name="related-topics"></a>相关主题
[USB 电源管理](usb-power-management.md)  



