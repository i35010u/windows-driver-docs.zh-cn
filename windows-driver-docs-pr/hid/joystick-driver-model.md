---
title: 游戏杆驱动程序模型
description: 游戏杆驱动程序模型
ms.assetid: 5bd41377-37ae-4ca7-8a6d-93311511ef4e
keywords:
- 游戏杆 WDK HID，驱动程序模型
- 虚拟游戏杆驱动程序 WDK HID，驱动程序模型
- VJoyD WDK HID，驱动程序模型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bceba0389623f9c6c3a5bfce7181a3cab9e60cb2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566780"
---
# <a name="joystick-driver-model"></a>游戏杆驱动程序模型





游戏杆驱动程序模型的最重要目标之一是提供及时访问游戏杆的信息。 两个驱动程序提供的 Windows 95/98/我游戏杆服务： 16 位 ring 3 驱动程序 (Msjstick.drv) 和一个 32 位 ring 0 驱动程序 (Vjoyd.vxd)。 Msjstick.drv 驱动程序提供基本服务，例如注册表更新和上限信息;Vjoyd.vxd 提供轮询服务。

游戏杆的 API 为 16 位应用程序在 Windows 95/98/我，并通过 Winmm.dll DLL 的 32 位应用程序提供通过 Mmsystem.dll 动态链接库 (DLL)。 Mmsystem.dll Msjstick.drv 与通信的所有游戏杆服务 （Msjstick.drv 与 Vjoyd.vxd 提供的轮询服务进行通信）。 Winmm.dll 直接与 Vjoyd.vxd 轮询服务进行通信并不是时间关键的基本服务到 Mmsystem.dll thunk。

在 DirectX 5.0 DirectInput 启动，并提供了备选的、 基于 COM 的 API。 Dinput.dll 使用 VJoyD，并且如果可用，人体学接口设备 (HID) 堆栈，以提供的轮询服务。 HID 的设备还会通过 VJoyD 报告，以便使用较旧的 API 的应用程序仍然能够读取新设备。 OEM 可以是任一 DLL 加载的 Dinput.dll 或扩展的 VJoyD 微型驱动程序，提供的驱动程序处理强制反馈。

 

 




