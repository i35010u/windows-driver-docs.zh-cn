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
ms.openlocfilehash: dbdb0c8235e53c71aefe84e397d0288055dce0de
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332282"
---
# <a name="obtaining-a-device-interface-name"></a>获取设备接口名称


## <span id="obtaining_a_device_interface_name"></span><span id="OBTAINING_A_DEVICE_INTERFACE_NAME"></span>


在 Windows Me 和 Windows 2000 和更高版本、 Windows 多媒体函数**waveInMessage**， **waveOutMessage**， **midiInMessage**， **midiOutMessage**，并**mixerMessage**可以检索设备的设备接口名称。 此信息可为需要 waveIn、 waveOut、 midiIn、 midiOut 或混音器 API 的外部设备进行标识的应用程序。 在这些 Api 之一，则设备 ID 就足够了。

插 manager 会生成设备接口名称来唯一标识它枚举每个设备。 应用程序应将包含一个设备接口名称作为不透明的字符串。 有关设备接口的详细信息，请参阅[简介设备接口](https://msdn.microsoft.com/library/windows/hardware/ff549460)。

标头文件 Mmddk.h 定义为了获取设备接口名称的两个消息常量：

[**DRV\_QUERYDEVICEINTERFACESIZE**](https://msdn.microsoft.com/library/windows/hardware/ff536364)

[**DRV\_QUERYDEVICEINTERFACE**](https://msdn.microsoft.com/library/windows/hardware/ff536363)

第一条消息获取以字节为单位保存包含设备接口名称的字符串所需的缓冲区的大小。 第二条消息中检索所需大小的缓冲区中的名称字符串。

系统会截获并处理了 DRV\_QUERYDEVICEINTERFACESIZE 和 DRV\_QUERYDEVICEINTERFACE 消息，而不必将消息发送到设备驱动程序。

第一个参数*xxx*消息函数是调用方必须转换为合适的句柄类型的设备 ID:HWAVEIN、 HWAVEOUT、 HMIDIIN、 HMIDIOUT 或 HMIXER。 有关详细信息*xxx*消息的函数，请参见[System-Intercepted 设备的消息](system-intercepted-device-messages.md)。

 

 




