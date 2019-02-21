---
title: 系统截获设备的消息
description: 系统截获设备的消息
ms.assetid: 5cf1c9a6-e56f-4358-933f-e8aa2ad1b1da
keywords:
- 对旧设备 WDK 音频设备的消息
- WDM 音频扩展 WDK，系统截获设备的消息
- 系统截获设备消息 WDK 音频
- 消息 WDK 音频
- 被拦截的设备的消息 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4623a07cb6a70873934bcfcab66b99e95ca28590
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520159"
---
# <a name="system-intercepted-device-messages"></a>系统截获设备的消息


## <span id="system_intercepted_device_messages"></span><span id="SYSTEM_INTERCEPTED_DEVICE_MESSAGES"></span>


以下 Windows 多媒体函数提供一种方法的调用方将消息传递到旧的音频设备：

-   [**waveInMessage**](https://msdn.microsoft.com/library/windows/desktop/dd743846)

-   [**waveOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd743865)

-   [**midiInMessage**](https://msdn.microsoft.com/library/windows/desktop/dd798457)

-   [**midiOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd798475)

-   [**mixerMessage**](https://msdn.microsoft.com/library/windows/desktop/dd757307)

-   [**auxOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd756716)

直接由设备驱动程序，这些设备的消息的一些处理，一些由系统处理代表设备。

本部分讨论仅由系统截获和处理而无需不断传递到设备驱动程序的消息。 系统截获消息可以获取有关语音通信或一般音频使用首选的设备。 此外，系统截获消息可以提供有关特定设备的以下信息：

-   **设备接口名称**

    有关设备接口名称的信息，请参阅[简介设备接口](https://msdn.microsoft.com/library/windows/hardware/ff549460)。

-   **设备的即插 devnode 号**

    Devnodes 有关的信息，请参阅[设备树](https://msdn.microsoft.com/library/windows/hardware/ff543194)。

-   **设备是否可以使用映射器**

    一个映射器通过将应用程序的要求映射到其中一个可用的设备在系统中选择适当的设备。 有关映射器的详细信息，请参阅 Microsoft Windows SDK 文档。

有关其他类型的设备的消息的信息，请参阅 Windows SDK 文档。

*Xxx*消息函数具有以下语法：

```cpp
DWORD XxxMessage(
<device ID>,
    UINT  uMsg,
    DWORD_PTR  dwParam1,
    DWORD_PTR  dwParam2
    );
```

第一个参数是设备 id。 [ **AuxOutMessage** ](https://msdn.microsoft.com/library/windows/desktop/dd756716)函数定义指定此参数的类型 UINT，按预期方式。 但是中的情况下[ **waveInMessage**](https://msdn.microsoft.com/library/windows/desktop/dd743846)， [ **waveOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd743865)， [ **midiInMessage**](https://msdn.microsoft.com/library/windows/desktop/dd798457)， [ **midiOutMessage**](https://msdn.microsoft.com/library/windows/desktop/dd798475)，或[ **mixerMessage**](https://msdn.microsoft.com/library/windows/desktop/dd757307)，调用方必须强制转换来处理类型的设备 IDHWAVEIN、 HWAVEOUT、 HMIDIIN、 HMIDIOUT 或 HMIXER，分别。 请注意，如果调用方提供有效的句柄，而不是此参数的设备 ID，该函数失败，将返回错误代码 MMSYSERR\_NOSUPPORT。

*UMsg*参数指定的消息值 (例如， [ **DRV\_QUERYDEVICEINTERFACE**](https://msdn.microsoft.com/library/windows/hardware/ff536363))。 有关特定于驱动程序的消息的列表，请参阅标头文件 Mmddk.h。

参数的含义*dwParam1*并*dwParam2*取决于消息。 例如，特定的消息可能会要求*dwParam1* ULONG 值; 调用方必须强制转换该值，以类型 DWORD\_PTR 以满足函数定义。

该函数将返回 MMERR\_NOERROR 如果调用成功，或如果不是错误状态代码。

有关详细信息*Xxx*消息函数，请参阅 Windows SDK 文档。

标头文件 Mmddk.h 定义以下系统截获设备的消息：

[**DRV\_QUERYDEVICEINTERFACE**](https://msdn.microsoft.com/library/windows/hardware/ff536363)

有关详细信息，请参阅[获取设备接口名称](obtaining-a-device-interface-name.md)。

[**DRV\_QUERYDEVICEINTERFACESIZE**](https://msdn.microsoft.com/library/windows/hardware/ff536364)

有关详细信息，请参阅**获取设备接口名称**。

[**DRV\_QUERYDEVNODE**](https://msdn.microsoft.com/library/windows/hardware/ff536365)

查询的设备的 devnode 号。

[**DRV\_QUERYMAPPABLE**](https://msdn.microsoft.com/library/windows/hardware/ff536366)

查询设备是否可以使用映射器。

[**DRVM\_MAPPER\_CONSOLEVOICECOM\_GET**](https://msdn.microsoft.com/library/windows/hardware/ff536361)

有关详细信息，请参阅[首选语音通信设备 ID](preferred-voice-communications-device-id.md)。

[**DRVM\_MAPPER\_PREFERRED\_GET**](https://msdn.microsoft.com/library/windows/hardware/ff536362)

有关详细信息，请参阅[访问首选设备 ID](accessing-the-preferred-device-id.md)。

 

 




