---
title: 微型驱动程序提供的回调
description: 微型驱动程序提供的回调
ms.assetid: df5bbc1c-988f-4e07-9783-4f380f85c2b6
keywords:
- 游戏杆 WDK HID，回调
- 虚拟游戏杆驱动程序 WDK HID，回调
- VJoyD WDK HID 回调
- 回调 WDK 游戏杆
- 轮询 WDK 游戏杆
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3f3cbf1b6f41f9cfe73584847a40aa24a6e8b1d9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63372972"
---
# <a name="minidriver-supplied-callbacks"></a>微型驱动程序提供的回调





游戏杆硬件不轮询或使用了非标准轮询要求时可以实现微型驱动程序 （它必须是 VxD） 该 VJoyD 加载该类型的设备正在使用中。 VJoyD 也会调用微型驱动程序可以访问的位置和按钮的信息。 游戏杆微型驱动程序不需要而不提供任何接口来处理标准 SYS\_动态\_设备\_INIT 和 SYS\_动态\_设备\_退出消息当加载和卸载，设备和用于定义和注册四个特定于游戏杆的回调。 除了此原始接口提供支持，DirectX 5.0 和更高版本 VJoyD 还支持的扩展的接口。 扩展的接口允许注册新的回调，以支持轮询，强制的反馈和热插拔的游戏杆。

根据请求从 Msjstick.drv，VJoyD 检查微型驱动程序，应加载和卸载。 Msjstick.drv 使它可以处理每个设备的请求和 joyConfigChanged 时接收调用。 为它在处理每个设备初始化 Msjstick.drv**正常**启动序列，这意味着，某些设备和服务可能对微型驱动程序不可用时加载它。 因为 VJoyD 时分配给大量游戏杆; 加载微型驱动程序不在应用程序需要使用该设备，应保持在最低限度的处理。 只是因为加载的 VxD，不应启动后台处理、 共享的资源使用情况或大型内存分配。 VJoyD 开头 DirectX 5.0 中，并在后面的阶段中引导过程比原始其初始加载的微型驱动程序。

 

 




