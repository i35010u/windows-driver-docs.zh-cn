---
title: 旧版音频设备消息
description: 旧版音频设备消息
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 589251a97a80d537b07d0f471fa2cbd62648e264
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801051"
---
# <a name="legacy-audio-device-messages"></a>旧版音频设备消息


## <span id="ddk_legacy_audio_device_messages_ks"></span><span id="DDK_LEGACY_AUDIO_DEVICE_MESSAGES_KS"></span>


以下 Windows 多媒体函数提供了一种方法，供调用方将消息传递到旧版音频设备：

-   **waveInMessage**

-   **waveOutMessage**

-   **midiInMessage**

-   **midiOutMessage**

-   **mixerMessage**

-   **auxOutMessage**

其中一些设备消息由设备驱动程序直接处理，一些则由系统代表设备进行处理。

本节仅介绍系统拦截的消息，并在不传递到设备驱动程序的情况下进行处理。 有关详细信息，请参阅 [系统拦截的设备消息](./system-intercepted-device-messages.md)。

本节中所述的每条消息都有效，可用于前面列表中的六个 *xxx* 消息函数中的一个或多个。

本部分介绍以下消息：

[**WINSPOOL.DRV \_ QUERYDEVICEINTERFACE**](/previous-versions/windows/hardware/drivers/ff536363(v=vs.85))

[**WINSPOOL.DRV \_ QUERYDEVICEINTERFACESIZE**](/previous-versions/windows/hardware/drivers/ff536364(v=vs.85))

[**WINSPOOL.DRV \_ QUERYDEVNODE**](/previous-versions/windows/hardware/drivers/ff536365(v=vs.85))

[**WINSPOOL.DRV \_ QUERYMAPPABLE**](/previous-versions/windows/hardware/drivers/ff536366(v=vs.85))

[**DRVM \_ 映射器 \_ CONSOLEVOICECOM \_ 获取**](/previous-versions/windows/hardware/drivers/ff536361(v=vs.85))

[**DRVM \_ 映射器 \_ 首选 \_ GET**](/previous-versions/windows/hardware/drivers/ff536362(v=vs.85))

 

