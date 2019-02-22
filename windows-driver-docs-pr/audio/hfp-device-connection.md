---
title: HFP 设备连接
description: HFP 设备连接本主题将讨论如何确定音频系统和句柄 Bluetooth 连接状态信息无配置文件 (HFP) 设备。
ms.assetid: 29B33A3F-63BB-4E1E-B245-E90372A7812F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 673930dc731aa5cfe7ae575372e6c65feb1eb167
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554153"
---
# <a name="hfp-device-connection"></a>HFP 设备连接


HFP 设备连接本主题将讨论如何确定音频系统和句柄 Bluetooth 连接状态信息无配置文件 (HFP) 设备。

根据需要为所有音频驱动程序，音频驱动程序必须支持[ **KSPROPERTY\_JACK\_说明**](https://msdn.microsoft.com/library/windows/hardware/ff537364)。 音频驱动程序维护*IsConnected*字段筛选器工厂上下文中。 音频驱动程序使用此值时处理**KSPROPERTY\_JACK\_说明**属性。

当[ **IOCTL\_BTHHFP\_设备\_获取\_连接\_状态\_更新**](https://msdn.microsoft.com/library/windows/hardware/dn265106)成功完成，随后将音频驱动程序更新*IsConnected*使用新的连接状态。 如果状态已更改，音频驱动程序将引发[ **KSEVENT\_PINCAPS\_JACKINFOCHANGE** ](https://msdn.microsoft.com/library/windows/hardware/ff537134)事件，这会导致音频系统来重新评估的连接状态。 然后，音频驱动程序调用的另一个实例**IOCTL\_BTHHFP\_设备\_获取\_连接\_状态\_更新**以便接收下一步的状态更改。 如果没有更早的状态更改，它是请求仍挂起，请此第二次调用将失败，音频驱动程序不会更新及其连接状态，并不会再发出请求的状态更改信息。

如中所述[内核流式处理注意事项](kernel-streaming-considerations.md)，音频驱动程序必须支持[ **KSPROPERTY\_ONESHOT\_重新连接**](https://msdn.microsoft.com/library/windows/hardware/ff537369)和[**KSPROPERTY\_ONESHOT\_断开连接**](https://msdn.microsoft.com/library/windows/hardware/hh706181)，并为这些属性的处理程序必须发送 REQUESTCONNECT 和 REQUESTDISCONNECT Ioctl 分别 HFP 驱动程序。 这些 Ioctl 快速完成，并且音频驱动程序需要准备好响应返回的结果。

以下是一些其他蓝牙音频设备与连接相关因素的音频驱动程序开发人员必须了解。

## <a name="span-idstreamchannelspanspan-idstreamchannelspanspan-idstreamchannelspanstream-channel"></a><span id="Stream_channel"></span><span id="stream_channel"></span><span id="STREAM_CHANNEL"></span>Stream 通道


Stream 频道表示无线带宽的音频驱动程序的分配。 大多数情况下，这是 SCO 通道。 但是，某些管理 SCO 通道状态的详细信息进行处理完全在 HFP 驱动程序。 这包括的示例远程断开连接的可能是由于调用方案 HF 其中启动传输音频到可用性组 （其中 PC 充当的角色的可用性组在这种情况下）。

## <a name="span-idaudiofilterpinstatesspanspan-idaudiofilterpinstatesspanspan-idaudiofilterpinstatesspanaudio-filter-pin-states"></a><span id="Audio_filter_pin_states"></span><span id="audio_filter_pin_states"></span><span id="AUDIO_FILTER_PIN_STATES"></span>音频筛选器 pin 状态


音频驱动程序实现 KS pin 状态处理程序 （类似于 AVStrMiniPinSetDeviceState） 的两个 KS pin。 需要为上述这些插针，以将数据传输将以无线方式 SCO 流通道。 当这些引脚之一将转换为 KSSTATE\_ACQUIRE，音频驱动程序打开通道发送[ **IOCTL\_BTHHFP\_流\_打开**](https://msdn.microsoft.com/library/windows/hardware/dn265122)HFP 驱动程序。 这是一个异步调用，可能需要几秒钟才能完成。 音频驱动程序不需要实现自己的超时机制，应等到 IOCTL 完成，然后完成转换到 KSSTATE\_ACQUIRE。

这两个 KS pin 时转换到 KSSTATE\_停止，音频驱动程序将发送[ **IOCTL\_BTHHFP\_流\_关闭**](https://msdn.microsoft.com/library/windows/hardware/dn265120) HFP 驱动程序。 这将完成快速。

若要确定何时发送**IOCTL\_BTHHFP\_流\_打开**并**IOCTL\_BTHHFP\_流\_关闭**，音频驱动程序可以使用简单的引用计数机制来跟踪要求 SCO 流通道的 pin 数。 音频驱动程序会打开和关闭 SCO 流通道的引用计数从 0 更改为 1 时。

上**IOCTL\_BTHHFP\_流\_打开**，HFP 驱动程序会请求 SCO 通道，如果未打开，并完成请求的结果与 SCO 请求。 上**IOCTL\_BTHHFP\_流\_关闭**HFP 驱动程序请求 SCO 通道断开连接，如果打开一个。

## <a name="span-idremotescoconnectanddisconnectspanspan-idremotescoconnectanddisconnectspanspan-idremotescoconnectanddisconnectspanremote-sco-connect-and-disconnect"></a><span id="Remote_SCO_connect_and_disconnect"></span><span id="remote_sco_connect_and_disconnect"></span><span id="REMOTE_SCO_CONNECT_AND_DISCONNECT"></span>远程 SCO 连接和断开连接


在远程的 SCO 断开连接，如果 Stream 通道已关闭，HFP 驱动程序没有任何影响。 如果打开 Stream 通道 HFP 驱动程序将启动重新连接计时器。 在计时器过期时，如果 SCO 仍断开连接和 Stream 通道仍处于打开状态，该驱动程序将请求 SCO 通道。 请注意 SCO 断开连接，因此在此期间将音频中的存在间隔时，将任何音频数据传输将以无线方式。 如果 SCO 请求失败，则 HFP 驱动程序发出信号，指示 Stream 通道状态更改为音频驱动程序通过完成任何调用[ **IOCTL\_BTHHFP\_流\_获取\_状态\_更新**](https://msdn.microsoft.com/library/windows/hardware/dn265121)。 这应该很少见，因为远程 SCO 断开连接通常与 HF 设备请求到的传输调用音频的音频的网关相关联。 音频驱动程序应考虑这一中间流错误情况。

此过程允许将 VoIP 应用程序从 CallButtons API 接收的音频传输回调，完全释放 HFP 终结点，而不是导致流式处理的错误上其音频资源的时间。

在远程 SCO 上连接，如果 Stream 通道是打开的驱动程序只需接受连接。 如果 Stream 通道已关闭，HFP 驱动程序接受连接，并且还将启动一个断开连接计时器。 断开连接计时器过期时，如果 SCO 仍处于连接状态和 Stream 通道仍然关闭，则该驱动程序会中断 SCO 连接。

此过程允许将 VoIP 应用程序从 CallButtons API 接收的音频传输回调，而不会过早地拒绝或 SCO 连接建立 HFP 终结点上的音频资源的时间。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关的主题
[理论上的操作](theory-of-operation.md)  



