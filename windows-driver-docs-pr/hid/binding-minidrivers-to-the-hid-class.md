---
title: 将微型驱动程序绑定到 HID 类
description: 本部分介绍系统提供的 HID 类驱动程序和 HID 微型驱动程序，其中 HIDClass 设备安装程序类中支持的设备的操作。
ms.assetid: 2B51E205-8EBB-413A-A317-0923FAB77F0E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 96c68a610802110ff174bbed2b2588e976afd72a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63390360"
---
# <a name="binding-minidrivers-to-the-hid-class"></a>将微型驱动程序绑定到 HID 类


本部分介绍系统提供的 HID 类驱动程序和 HID 微型驱动程序，这在 HIDClass 中支持的设备的操作[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)。

HID 类驱动程序提供的接口的较高级别驱动程序和用户模式应用程序用于访问支持的输入设备的 HID 集合。 HID 类驱动程序使用 HID 微型驱动程序来访问输入设备的硬件。 HID 微型驱动程序的抽象操作的输入的设备连接到该总线的端口。 HID 类驱动程序是链接到 HID 微型驱动程序导出驱动程序。 HID 微型驱动程序将其操作绑定到的 HID 类驱动程序，通过调用[ **HidRegisterMinidriver** ](https://msdn.microsoft.com/library/windows/hardware/ff539835)自行注册到的 HID 类驱动程序。

HID 类驱动程序和 HID 微型驱动程序的组合的操作将充当输入设备的 WDM 函数驱动程序和总线驱动程序的输入的设备支持的子设备 （HID 集合）。 这种设计使 USB HID 设备和非 USB 连接到端口或 USB 总线以外的总线的输入的设备的运行的 HID 类驱动程序。 基础的父设备操作的详细信息是透明的较高级别驱动程序或用户模式应用程序。

 

 




