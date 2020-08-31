---
title: 视频微型端口驱动程序初始化（Windows 2000 模型）
description: 视频微型端口驱动程序初始化（Windows 2000 模型）
ms.assetid: b18b5483-f11f-4533-9434-a3a4a30fb4b2
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，初始化
- 初始化视频微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0e74ad37415c7ac9946c83b9937e3671b3a3e8c
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063718"
---
# <a name="video-miniport-driver-initialization-windows-2000-model"></a>视频微型端口驱动程序初始化（Windows 2000 模型）


## <span id="ddk_video_miniport_driver_initialization_windows_2000_model__gg"></span><span id="DDK_VIDEO_MINIPORT_DRIVER_INITIALIZATION_WINDOWS_2000_MODEL__GG"></span>


在加载并初始化 NT 内核、 *HAL*和核心驱动程序（如 PCI 总线驱动程序）之后，会发生视频微型端口驱动程序初始化。 基本系统初始化顺序如下所示：

1.  加载并初始化 NT 内核和 HAL。

2.  加载并初始化核心驱动程序（如 PCI 总线驱动程序）。

3.  PCI 总线驱动程序从其每个子配置空间获取 PCI 资源信息、设备 ID 和供应商 ID，并将此信息报告给系统。

4.  如果 PnP 管理器识别设备和供应商 Id，则 i/o 管理器从已知位置加载相应的视频微型端口驱动程序和视频端口驱动程序。 如果 PnP 管理器无法识别这些 Id，则会提示用户输入微型端口驱动程序的位置，并从此位置加载该驱动程序。

5.  I/o 管理器调用微型端口驱动程序的 [**DriverEntry**](./driverentry-of-video-miniport-driver.md) 例程，其中包含两个系统提供的输入指针。 **DriverEntry** 使用驱动程序特定的值和特定于适配器的值分配和初始化 [**视频 \_ 硬件 \_ 初始化 \_ 数据**](/windows-hardware/drivers/ddi/video/ns-video-_video_hw_initialization_data) 结构，包括指向微型端口驱动程序的其他入口点的指针。 **DriverEntry** 还必须声明任何旧资源，这些资源是设备 PCI 配置空间中未列出的资源，但被设备解码。 有关详细信息，请参阅 [声明旧资源](claiming-legacy-resources.md) 。

6.  微型端口驱动程序的 **DriverEntry** 函数调用 [**VideoPortInitialize**](/windows-hardware/drivers/ddi/video/nf-video-videoportinitialize)。 **VideoPortInitialize** 对所有微型端口驱动程序都通用的微型端口驱动程序初始化执行这些方面。 例如，对于非 PnP 驱动程序， **VideoPortInitialize** 将验证微型端口驱动程序初始化视频 \_ HW \_ 初始化数据结构的部分、 \_ 初始化系统创建的设备对象的一些公共成员、为设备对象的设备扩展分配内存，以及收集和存储设备扩展中的相关信息。 有关设备扩展的更多详细信息，请参阅 [视频微型端口驱动程序的设备扩展 (Windows 2000 模型) ](video-miniport-driver-s-device-extension--windows-2000-model-.md) 。 对于 PnP 驱动程序，将在稍后发生与设备对象相关的操作。

7.  当 **VideoPortInitialize** 返回时， **DriverEntry** 将 **VideoPortInitialize** 的返回值传播回调用方。 小型小型驱动程序编写器不应假设 **VideoPortInitialize**返回的值。

此时，系统已加载并初始化了视频微型端口驱动程序。 下一步是 PnP 管理器启动设备。 有关详细信息，请参阅 [启动视频微型端口驱动程序的设备](starting-the-device-of-the-video-miniport-driver.md) 。

 

