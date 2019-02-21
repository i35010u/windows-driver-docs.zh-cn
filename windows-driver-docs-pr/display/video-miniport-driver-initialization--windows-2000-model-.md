---
title: 视频微型端口驱动程序初始化 （Windows 2000 模式）
description: 视频微型端口驱动程序初始化 （Windows 2000 模式）
ms.assetid: b18b5483-f11f-4533-9434-a3a4a30fb4b2
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，初始化
- 初始化微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45204b0068b630bd440580ee9b3e6b9c6e40ca89
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546177"
---
# <a name="video-miniport-driver-initialization-windows-2000-model"></a>视频微型端口驱动程序初始化 （Windows 2000 模式）


## <span id="ddk_video_miniport_driver_initialization_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_INITIALIZATION_WINDOWS_2000_MODEL__GG"></span>


微型端口驱动程序初始化之后 NT 内核*HAL*，和核心驱动程序，如 PCI 总线驱动程序，就会加载和初始化。 基本系统初始化顺序发生，如下所示：

1.  NT 内核和 HAL 加载和初始化。

2.  核心驱动程序，如 PCI 总线驱动程序加载和初始化。

3.  PCI 总线驱动程序从每个其子级的 PCI 配置空间获取 PCI 资源信息和设备 ID 和供应商 ID，并报告此信息发送回系统。

4.  如果 PnP 管理器识别的设备和供应商 Id，I/O 管理器将从已知位置加载相应的微型端口驱动程序和视频端口驱动程序。 如果 PnP 管理器无法识别的 Id，它将提示用户输入的微型端口驱动程序的位置，并将其加载从该位置。

5.  I/O 管理器调用微型端口驱动程序[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff556159)具有两个系统提供的例程的输入指针。 **DriverEntry**分配并初始化[**视频\_HW\_初始化\_数据**](https://msdn.microsoft.com/library/windows/hardware/ff570505)具有特定于驱动程序的结构和特定于适配器的值，包括指向微型端口驱动程序的其他入口点。 **DriverEntry**还必须声明任何旧的资源，哪些是设备的 PCI 配置空间中未列出这些资源但的解码设备。 请参阅[声明旧资源](claiming-legacy-resources.md)有关详细信息。

6.  微型端口驱动程序**DriverEntry**函数调用[ **VideoPortInitialize**](https://msdn.microsoft.com/library/windows/hardware/ff570320)。 **VideoPortInitialize**执行普遍适用于所有微型端口驱动程序微型端口驱动程序初始化的那些方面。 例如，对于非 PnP 驱动程序**VideoPortInitialize**验证部分的微型端口驱动程序初始化视频\_HW\_初始化\_数据结构初始化的一些系统创建设备对象的公共成员为设备扩展的设备对象分配内存并收集并将相关的信息存储在设备扩展。 请参阅[视频微型端口驱动程序设备扩展 （Windows 2000 模式）](video-miniport-driver-s-device-extension--windows-2000-model-.md)有关设备扩展的详细信息。 即插即用驱动程序，请与对象相关的设备操作发生在更高版本时。

7.  当**VideoPortInitialize**返回时， **DriverEntry**传播的返回值**VideoPortInitialize**回调用方。 微型端口驱动程序编写人员应作出任何假设返回的值**VideoPortInitialize**。

此时，系统已加载并初始化微型端口驱动程序。 下一步是为要启动设备的即插即用管理器。 请参阅[启动视频微型端口驱动程序设备](starting-the-device-of-the-video-miniport-driver.md)有关详细信息。

 

 





