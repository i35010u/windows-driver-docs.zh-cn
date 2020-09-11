---
description: 本主题介绍有关在客户端驱动程序中实施远程唤醒功能的最佳实践。
title: 远程唤醒 USB 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: aaa08a6801d914d3af516941b32cc394494c49bf
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010613"
---
# <a name="remote-wakeup-of-usb-devices"></a>远程唤醒 USB 设备


本主题介绍有关在客户端驱动程序中实施远程唤醒功能的最佳实践。

如果 USB 设备在挂起时可以响应外部唤醒信号，则称为具有 *远程唤醒* 功能。 具有远程唤醒功能的设备的示例包括：鼠标、键盘、USB 集线器、调制解调器 (唤醒) 、Nic、插入时唤醒。 所有这些设备都能产生远程唤醒信号。 不能生成远程唤醒信号的设备包括视频相机、大容量存储设备、音频设备和打印机。

支持远程唤醒信号的设备驱动程序必须发出 [**IRP \_ MN \_ wait \_ 唤醒**](../kernel/irp-mn-wait-wake.md) irp，也称为等待唤醒 irp，以 arm 设备进行远程唤醒。 等待唤醒机制在 [支持具有唤醒功能的设备](../kernel/supporting-devices-that-have-wake-up-capabilities.md)的部分中进行了介绍。

## <a name="when-does-the-system-enable-remote-wakeup-on-a-usb-leaf-device"></a>系统何时启用 USB 叶设备上的远程唤醒？


在 USB 术语中，在设置了 USB 设备的设备 \_ 远程唤醒功能时，会为其启用远程唤醒 \_ 。 USB 规范指定主机软件必须在设备上 "只是之前" 设置远程唤醒功能，使设备进入睡眠状态。

出于此原因，在接收到设备的等待唤醒 IRP 后，USB 堆栈不会 \_ 在设备上设置设备远程 \_ 唤醒功能。 相反，它会一直等待，直到收到 [**IRP \_ MN \_ SET \_ 电源**](../kernel/irp-mn-set-power.md) 请求，将设备的 WDM 设备状态更改为 D1/D2。 在大多数情况下，当 USB stack 收到此请求时，它会在设备上设置远程唤醒功能，并通过挂起设备的上游端口来使设备进入睡眠状态。 当你设计和调试驱动程序时，应记住，武装是用于唤醒软件的 USB 设备与等待唤醒 IRP 之间的松关系，并通过设置远程唤醒功能武装设备在硬件中唤醒。

当设备收到将设备更改为 "D3" 睡眠状态的请求时，USB 堆栈不允许设备进行远程唤醒，因为根据 WDM 电源模式，D3 中的设备无法唤醒系统。

## <a name="why-does-attaching-or-detaching-my-device-produce-a-different-wakeup-behavior-in-windows-xp-and-windows-vista-and-later-versions-of-windows"></a>为什么附加或分离设备会在 Windows XP 和 Windows Vista 及更高版本的 Windows 中产生不同的唤醒行为？


WDM 电源模式 USB 实现的另一个独特方面是将 USB 集线器的武装用于远程唤醒。 在 Microsoft Windows XP 中，当 USB 设备唤醒时，主机控制器与 USB 设备之间的所有集线器设备都能唤醒。 这产生了惊人的结果，当睡眠设备分离时，它们会唤醒系统。

在 Windows Vista 和更高版本的 Windows 中，如果总线上的 USB 叶设备为唤醒提供，则 USB stack 还将对 USB 主机控制器进行唤醒，但它不一定是设备上游的任何 USB 集线器。 仅当 USB 堆栈配置为在附加和分离 (插/拨) 事件时唤醒系统时，USB 集线器驱动程序才会将集线器用于远程唤醒。

**注意**   UHCI (通用主机控制器接口) USB 主机控制器不区分远程唤醒信号和连接根集线器端口上的更改事件。 这意味着，如果 USB 设备连接到根集线器端口或断开与根集线器端口的连接，则系统始终会从低系统电源状态唤醒，前提是在 UHCI 控制器的后面至少有一个设备用于唤醒。

 

## <a name="related-topics"></a>相关主题
[USB 电源管理](usb-power-management.md)