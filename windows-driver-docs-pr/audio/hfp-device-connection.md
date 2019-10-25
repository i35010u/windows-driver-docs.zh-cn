---
title: HFP 设备连接
description: HFP 设备连接主题讨论音频系统如何确定和处理蓝牙免提配置文件（HFP）设备的连接状态信息。
ms.assetid: 29B33A3F-63BB-4E1E-B245-E90372A7812F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2feea23c231598f93d69b8c8f2d384e4be31139d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72831187"
---
# <a name="hfp-device-connection"></a>HFP 设备连接


HFP 设备连接主题讨论音频系统如何确定和处理蓝牙免提配置文件（HFP）设备的连接状态信息。

根据所有音频驱动程序的需要，音频驱动程序必须支持[**KSPROPERTY\_插孔\_说明**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-jack-description)。 音频驱动程序在筛选器工厂上下文中维护一个*connectionmultiplexer.isconnected*字段。 音频驱动程序在处理**KSPROPERTY\_插孔\_DESCRIPTION**属性时使用该值。

当[**IOCTL\_BTHHFP\_设备\_获取\_连接\_状态\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_connection_status_update)成功完成，则音频驱动程序将更新*connectionmultiplexer.isconnected* ，并显示新的连接状态。 如果状态已更改，则音频驱动程序会引发[**KSEVENT\_PINCAPS\_JACKINFOCHANGE**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksevent-pincaps-jackinfochange)事件，这将导致音频系统重新计算连接状态。 然后，音频驱动程序调用 **\_BTHHFP\_设备的 IOCTL 的另一个实例\_获取\_连接\_状态\_更新**以接收下一个状态更改。 如果以前的状态更改请求仍处于挂起状态，则第二次调用将失败，并且音频驱动程序不会更新其连接状态，也不会发出对状态更改信息的其他请求。

如[内核流式处理注意事项](kernel-streaming-considerations.md)中所述，音频驱动程序必须支持[**KSPROPERTY\_ONESHOT\_重新连接**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-oneshot-reconnect)和[**KSPROPERTY\_ONESHOT\_断开连接**](https://docs.microsoft.com/windows-hardware/drivers/audio/ksproperty-oneshot-disconnect)，并且这些属性的处理程序必须将 REQUESTCONNECT 和 REQUESTDISCONNECT IOCTLs 分别发送到 HFP 驱动程序。 这些 IOCTLs 很快就会完成，并且音频驱动程序需要准备好响应返回的结果。

下面是音频驱动程序开发人员必须知道的一些其他与蓝牙音频设备连接相关的因素。

## <a name="span-idstream_channelspanspan-idstream_channelspanspan-idstream_channelspanstream-channel"></a><span id="Stream_channel"></span><span id="stream_channel"></span><span id="STREAM_CHANNEL"></span>流通道


流通道表示音频驱动程序的无线带宽分配。 大多数情况下，这是 SCO 通道。 但在 HFP 驱动程序中，管理 SCO 通道状态的某些细节将完全处理。 这包括例如远程断开连接，这可能是由于调用 HF 启动了到 AG 的音频传输（在这种情况下，PC 扮演 AG 的角色）的情况。

## <a name="span-idaudio_filter_pin_statesspanspan-idaudio_filter_pin_statesspanspan-idaudio_filter_pin_statesspanaudio-filter-pin-states"></a><span id="Audio_filter_pin_states"></span><span id="audio_filter_pin_states"></span><span id="AUDIO_FILTER_PIN_STATES"></span>音频筛选器 pin 状态


音频驱动程序为两个 KS 引脚实现了一个 KS pin 状态处理程序（类似于 AVStrMiniPinSetDeviceState）。 其中任何一个 pin 都需要 SCO 流通道，才能通过无线传输数据。 当其中任何一个 pin 转换为 KSSTATE\_获取时，音频驱动程序会通过将[**IOCTL 发送\_BTHHFP\_流\_打开**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_open)HFP 驱动程序来打开通道。 这是一个异步调用，可能需要几秒钟才能完成。 音频驱动程序无需实现其自己的超时机制，应等待 IOCTL 完成，然后才能完成到 KSSTATE\_获取的转换。

当两个 KS pin 都转换为 KSSTATE 时\_停止时，音频驱动程序会将[**IOCTL\_BTHHFP\_流\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_close)到 HFP 驱动程序附近。 这会迅速完成。

若要确定何时发送**IOCTL\_BTHHFP\_stream\_打开**和**ioctl\_BTHHFP\_流\_关闭**，则音频驱动程序可以使用简单的引用计数机制跟踪需要 SCO 流通道。 当引用计数从0更改为1时，音频驱动程序会打开并关闭 SCO 流通道。

在**IOCTL\_BTHHFP\_STREAM\_打开**时，HFP 驱动程序会请求 sco 通道（如果尚未打开），并使用 sco 请求的结果完成请求。 在**IOCTL\_BTHHFP\_STREAM\_关闭**HFP 驱动程序请求 SCO 通道断开连接（如果有）。

## <a name="span-idremote_sco_connect_and_disconnectspanspan-idremote_sco_connect_and_disconnectspanspan-idremote_sco_connect_and_disconnectspanremote-sco-connect-and-disconnect"></a><span id="Remote_SCO_connect_and_disconnect"></span><span id="remote_sco_connect_and_disconnect"></span><span id="REMOTE_SCO_CONNECT_AND_DISCONNECT"></span>远程 SCO 连接和断开连接


在远程 SCO 断开连接上，如果流通道已关闭，HFP 驱动程序将不执行任何操作。 如果打开流通道，HFP 驱动程序将启动重新连接计时器。 当计时器过期时，如果 SCO 仍断开连接并且流通道仍处于打开状态，则驱动程序将请求 SCO 通道。 请注意，当 SCO 断开连接时，不会通过无线传输音频数据，因此在这段时间内音频会出现间隙。 如果 SCO 请求失败，则 HFP 驱动程序将通过完成任何调用的 IOCTL\_BTHHFP\_STREAM，将流通道状态更改通知给音频驱动程序[ **\_获取\_状态\_更新**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_get_status_update)。 这应该很少见，因为远程 SCO 断开连接通常与请求将电话音频传输到音频网关的 HF 设备相关联。 音频驱动程序应将这种情况视为中间流错误情况。

此过程允许 VoIP 应用程序从 CallButtons API 接收音频传输回拨，并在 HFP 终结点上完全释放其音频资源，而不是导致流式处理错误。

在远程 SCO 连接上，如果流通道为打开状态，则驱动程序只接受连接。 如果流通道已关闭，则 HFP 驱动程序会接受连接，并且还会启动断开连接计时器。 当断开连接计时器过期时，如果 SCO 仍处于连接状态并且流通道仍处于关闭状态，则驱动程序将中断 SCO 连接。

此过程允许 VoIP 应用程序从 CallButtons API 接收音频传输回拨，并在 HFP 终结点上建立音频资源，而无需提前拒绝或关闭 SCO 连接。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[操作理论](theory-of-operation.md)  



