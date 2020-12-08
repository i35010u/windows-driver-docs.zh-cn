---
title: 操作理论
description: 这一操作理论说明了新 Windows 8.1 的内部工作原理。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 605b08b39fea733cec0646fbf2ac2cbf53b87192
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800525"
---
# <a name="theory-of-operation"></a>操作理论


这一操作理论说明了新 Windows 8.1 支持蓝牙绕过音频流的内部工作原理。

当蓝牙音频处于旁路模式时，音频控制路径会通过与蓝牙控制器的某些其他硬件连接，而不是通过主机控制器接口 (HCI) 。 此其他硬件连接通常 I2S，但可以是由蓝牙主机控制器确定的任何接口。 这组主题将此连接称为 "跳过" 或 "sideband" 连接。

当通过绕过连接进行音频 i/o 时，面向无线同步连接 (SCO) 音频流仍通过 HCI 进行管理。 Windows 8 提供了一个蓝牙 Hands-Free 配置文件 (HFP) 驱动程序，以隐藏管理 SCO 连接和 Hands-Free 配置文件的其他方面的大部分复杂性。 但是，自定义音频驱动程序控制 Windows 与绕过连接之间的音频数据 i/o。

HFP 驱动程序与自定义控制驱动程序的音频 i/o 数据之间的角色分离意味着必须在 Windows HFP 驱动程序和自定义音频驱动程序之间建立有效的通信。 此通信由从自定义音频驱动程序传递到 Windows HFP 驱动程序的一组 IOCTLs 处理。

通常，绕过连接本身始终存在。 PnP 服务始终枚举包含此连接的硬件，然后加载所需的音频驱动程序。 但是，如果至少有一个 HFP 耳机配对，则音频系统可能会也可能不会有任何 HFP 耳机配对，并且绕过连接将非常有用。

对于每个配对的 HFP 设备，Windows HFP 驱动程序在 GUID \_ DEVINTERFACE \_ 蓝牙 \_ HFP \_ SCO \_ HCIBYPASS 接口类中注册并启用设备接口。 因此，适用于 HFP 设备的情况如下：

-   当 Windows 在启动)  (正常情况下激活 HFP 驱动程序时，HFP 驱动程序将为每个配对的 HFP 设备注册并启用一个接口。

-   当 HFP 设备第一次配对，Windows 已启动并正在运行时，HFP 驱动程序将注册并启用设备接口。

-   如果有 n 个配对的 HFP 设备，则 Windows HFP 驱动程序将注册设备接口的 n 个实例。

-   删除配对的 HFP 设备后，Windows HFP 驱动程序将禁用该设备接口。

-   当 Windows 在关闭或重新启动)  (正常时，会关闭 HFP 驱动程序，HFP 驱动程序将禁用每个配对的 HFP 设备的接口。

-   音频驱动程序必须随时处理接口的多个到达和删除，而不只是在启动或关闭过程中处理。

以下主题提供了有关连接生命周期和 HFP 设备及其音频驱动程序的某些设计功能的详细信息。

[HFP 设备启动](startup.md)

[HFP 设备连接](hfp-device-connection.md)

[HFP 设备删除](removal.md)

[内核流式处理注意事项](kernel-streaming-considerations.md)

[音频终结点容器 ID](audio-endpoint-container-id.md)

[I2S 和 SCO 资源的管理](management-of-i2s-and-sco-resources.md)

 

 




