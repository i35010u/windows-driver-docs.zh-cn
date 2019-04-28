---
title: 旧版音频设备消息
description: 旧版音频设备消息
ms.assetid: d8b2807b-e72f-4f72-8a83-5700bc0239dc
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a229b443bbe79263e6d2f65fe87f27f87484662e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63332425"
---
# <a name="legacy-audio-device-messages"></a>旧版音频设备消息


## <span id="ddk_legacy_audio_device_messages_ks"></span><span id="DDK_LEGACY_AUDIO_DEVICE_MESSAGES_KS"></span>


以下 Windows 多媒体函数提供一种方法的调用方将消息传递到旧的音频设备：

-   **waveInMessage**

-   **waveOutMessage**

-   **midiInMessage**

-   **midiOutMessage**

-   **mixerMessage**

-   **auxOutMessage**

直接由设备驱动程序，这些设备的消息的一些处理，一些由系统处理代表设备。

本部分介绍由系统截获和处理而无需不断传递到设备驱动程序的消息。 有关详细信息，请参阅[System-Intercepted 设备的消息](https://msdn.microsoft.com/library/windows/hardware/ff538507)。

在本部分中所述的每条消息是与一个或多个六个有效*xxx*消息前面列表中的函数。

本部分介绍以下消息：

[**DRV\_QUERYDEVICEINTERFACE**](https://msdn.microsoft.com/library/windows/hardware/ff536363)

[**DRV\_QUERYDEVICEINTERFACESIZE**](https://msdn.microsoft.com/library/windows/hardware/ff536364)

[**DRV\_QUERYDEVNODE**](https://msdn.microsoft.com/library/windows/hardware/ff536365)

[**DRV\_QUERYMAPPABLE**](https://msdn.microsoft.com/library/windows/hardware/ff536366)

[**DRVM\_MAPPER\_CONSOLEVOICECOM\_GET**](https://msdn.microsoft.com/library/windows/hardware/ff536361)

[**DRVM\_MAPPER\_PREFERRED\_GET**](https://msdn.microsoft.com/library/windows/hardware/ff536362)

 

 





