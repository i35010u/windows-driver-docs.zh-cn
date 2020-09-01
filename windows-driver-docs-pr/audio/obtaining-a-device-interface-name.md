---
title: 获取设备接口名称
description: 获取设备接口名称
ms.assetid: 2ad0bafa-c836-4dca-9287-72cdbddec7d0
keywords:
- WDM 音频扩展 WDK，设备接口名称
- 设备接口名称 WDK 音频
- 接口名称 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fccc3ae3e7d530db2b8a56003783e8ceaac2a4cc
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89208823"
---
# <a name="obtaining-a-device-interface-name"></a>获取设备接口名称


## <span id="obtaining_a_device_interface_name"></span><span id="OBTAINING_A_DEVICE_INTERFACE_NAME"></span>


在 Windows Me 和 Windows 2000 及更高版本中，Windows 多媒体函数 **waveInMessage**、 **waveOutMessage**、 **midiInMessage**、 **midiOutMessage**和 **mixerMessage** 可检索设备的设备接口名称。 此信息对于需要在 waveIn、waveOut、midiIn、midiOut 或混合器 API 之外识别设备的应用程序很有用。 在其中一个 Api 内，设备 ID 就已足够。

即插即用 manager 将生成一个设备接口名称，用于唯一标识它所枚举的每个设备。 应用程序应将包含设备接口名称的字符串视为不透明。 有关设备接口的详细信息，请参阅 [设备接口简介](../install/overview-of-device-interface-classes.md)。

标头文件 Mmddk 定义了两个消息常量，目的是获取设备接口名称：

[**WINSPOOL.DRV \_ QUERYDEVICEINTERFACESIZE**](/previous-versions/windows/hardware/drivers/ff536364(v=vs.85))

[**WINSPOOL.DRV \_ QUERYDEVICEINTERFACE**](/previous-versions/windows/hardware/drivers/ff536363(v=vs.85))

第一条消息获取包含设备接口名称的字符串所需的缓冲区大小（以字节为单位）。 第二条消息检索所需大小的缓冲区中的名称字符串。

系统会截获并处理 WINSPOOL.DRV \_ QUERYDEVICEINTERFACESIZE 和 Winspool.drv \_ QUERYDEVICEINTERFACE 消息，而不会将消息发送到设备驱动程序。

*Xxx*消息函数的第一个参数是设备 ID，调用方必须将其强制转换为相应的句柄类型： HWAVEIN、HWAVEOUT、HMIDIIN、HMIDIOUT 或 HMIXER。 有关 *xxx*消息函数的详细信息，请参阅 [系统拦截的设备消息](system-intercepted-device-messages.md)。

 

