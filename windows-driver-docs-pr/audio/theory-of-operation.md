---
title: 操作理论
description: 这一理论的操作主题介绍了新的 Windows 8.1 的内部工作原理。
ms.assetid: 5897946A-5319-404B-BE9E-91FF8801652F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bc30f92ce72ee1ebebf4762bae82dedb7ee15a03
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335235"
---
# <a name="theory-of-operation"></a>操作理论


这一理论的操作主题说明对于蓝牙旁路音频流的新 Windows 8.1 支持的内部工作原理。

时音频处于的蓝牙旁路模式，显示音频控件路径的流通过某些其他硬件连接到蓝牙控制器，而不是通过主机控制器接口 (HCI)。 此其他硬件连接通常是 I2S，但可将通过蓝牙主机控制器确定的任何接口。 此系列主题是指此连接为"绕过"或"旁带"连接。

通过绕过连接进行音频 I/O，同时仍通过 HCI 管理无线同步面向连接的 (SCO) 音频流。 Windows 8 提供的蓝牙免提配置文件 (HFP) 驱动程序以隐藏大部分的管理 SCO 连接，并且无需手动配置文件的其他方面的复杂性。 但是，自定义的音频驱动程序控制 Windows 和跳过连接之间的音频数据 I/O。

HFP 驱动程序和 I/O 的音频数据，自定义控件驱动程序的角色分离意味着，必须在 Windows HFP 驱动程序和自定义音频驱动程序之间建立有效的通信。 此通信由一系列 Ioctl，从自定义音频驱动程序传递给 Windows HFP 驱动程序处理。

通常不使用连接本身始终存在。 即插即用服务始终枚举的硬件，包括此连接，然后加载所需的音频驱动程序。 但是，音频系统可能会或可能不具有任何 HFP 耳机配对和跳过连接才有用至少一个 HFP 耳机配对。

对于每个配对的 HFP 设备，Windows HFP 驱动程序注册，并启用设备接口的 guid\_DEVINTERFACE\_蓝牙\_HFP\_SCO\_HCIBYPASS 接口类。 因此以下条件成立 HFP 设备：

-   当 Windows 激活 HFP 驱动程序 （通常在启动）、 HFP 驱动程序注册和启用每个接口配对 HFP 设备。

-   第一个 HFP 设备时，已与配对，Windows 已启动并正在运行，HFP 驱动程序注册并启用设备的接口。

-   如果有 n 个配对的 HFP 设备，Windows HFP 驱动程序注册的设备接口的 n 个实例。

-   删除配对的 HFP 设备后，Windows HFP 驱动程序禁用设备接口。

-   当 Windows 停止 HFP 驱动程序 （通常在关闭或重新启动） 时，HFP 驱动程序禁用每个配对 HFP 设备的接口。

-   音频驱动程序必须处理多个到达的请求和删除的接口在任何时候，而不仅仅是在启动或关机。

以下主题提供有关连接生命周期的详细信息和 HFP 设备和其音频驱动程序的某些设计功能。

[HFP 设备启动](startup.md)

[HFP 设备连接](hfp-device-connection.md)

[HFP 设备删除](removal.md)

[内核流式处理注意事项](kernel-streaming-considerations.md)

[音频的终结点，容器 ID](audio-endpoint-container-id.md)

[I2S 和 SCO 资源的管理](management-of-i2s-and-sco-resources.md)

 

 




