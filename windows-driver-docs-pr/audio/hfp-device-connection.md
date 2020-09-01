---
title: HFP 设备连接
description: HFP 设备连接主题讨论音频系统如何确定和处理蓝牙免提配置文件 (HFP) 设备的连接状态信息。
ms.assetid: 29B33A3F-63BB-4E1E-B245-E90372A7812F
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e94615e688afe6727ed90370b0b69021f033215e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209167"
---
# <a name="hfp-device-connection"></a>HFP 设备连接


HFP 设备连接主题讨论音频系统如何确定和处理蓝牙免提配置文件 (HFP) 设备的连接状态信息。

根据所有音频驱动程序的需要，音频驱动程序必须支持 [**KSPROPERTY \_ 插孔 \_ 说明**](./ksproperty-jack-description.md)。 音频驱动程序在筛选器工厂上下文中维护一个 *connectionmultiplexer.isconnected* 字段。 音频驱动程序在处理 **KSPROPERTY \_ 插孔 \_ 说明** 属性时使用此值。

如果 [**IOCTL \_ BTHHFP \_ 设备 \_ 获取 \_ 连接 \_ 状态 \_ 更新**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_device_get_connection_status_update) 成功完成，则音频驱动程序将更新 *connectionmultiplexer.isconnected* ，并显示新的连接状态。 如果状态已更改，则音频驱动程序会引发 [**KSEVENT \_ PINCAPS \_ JACKINFOCHANGE**](./ksevent-pincaps-jackinfochange.md) 事件，这将导致音频系统重新计算连接状态。 然后，音频驱动程序调用 **IOCTL \_ BTHHFP \_ 设备 \_ \_ \_ \_ ** 的另一个实例，以接收下一个状态更改。 如果以前的状态更改请求仍处于挂起状态，则第二次调用将失败，并且音频驱动程序不会更新其连接状态，也不会发出对状态更改信息的其他请求。

如 [内核流式处理注意事项](kernel-streaming-considerations.md)中所述，音频驱动程序必须支持 [**KSPROPERTY \_ ONESHOT \_ RECONNECT**](./ksproperty-oneshot-reconnect.md) 和 [**KSPROPERTY \_ ONESHOT \_ DISCONNECT**](./ksproperty-oneshot-disconnect.md)，并且这些属性的处理程序必须分别向 REQUESTCONNECT 驱动程序发送 REQUESTDISCONNECT IOCTLs 和 HFP。 这些 IOCTLs 很快就会完成，并且音频驱动程序需要准备好响应返回的结果。

下面是音频驱动程序开发人员必须知道的一些其他与蓝牙音频设备连接相关的因素。

## <a name="span-idstream_channelspanspan-idstream_channelspanspan-idstream_channelspanstream-channel"></a><span id="Stream_channel"></span><span id="stream_channel"></span><span id="STREAM_CHANNEL"></span>流通道


流通道表示音频驱动程序的无线带宽分配。 大多数情况下，这是 SCO 通道。 但在 HFP 驱动程序中，管理 SCO 通道状态的某些细节将完全处理。 这包括例如远程断开连接，这可能是由于调用 HF 启动了到 AG 的音频传输 (的情况，在这种情况下，计算机在此案例中扮演了 AG 的角色) 。

## <a name="span-idaudio_filter_pin_statesspanspan-idaudio_filter_pin_statesspanspan-idaudio_filter_pin_statesspanaudio-filter-pin-states"></a><span id="Audio_filter_pin_states"></span><span id="audio_filter_pin_states"></span><span id="AUDIO_FILTER_PIN_STATES"></span>音频筛选器 pin 状态


音频驱动程序实现了一个 KS pin 状态处理程序， (类似于两个 KS pin 的 AVStrMiniPinSetDeviceState) 。 其中任何一个 pin 都需要 SCO 流通道，才能通过无线传输数据。 当其中任一引脚转换为 KSSTATE 时 \_ ，音频驱动程序会通过将 [**IOCTL \_ BTHHFP \_ 流 \_ **](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_open) 发送到 HFP 驱动程序来打开通道。 这是一个异步调用，可能需要几秒钟才能完成。 音频驱动程序无需实现自己的超时机制，应等待 IOCTL 完成，然后才能完成过渡到 KSSTATE \_ 获取。

当两个 KS 引脚转换到 KSSTATE \_ 停止时，音频驱动程序会将 [**IOCTL \_ BTHHFP \_ 流 \_ **](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_close) 发送到 HFP 驱动程序附近。 这会迅速完成。

若要确定何时发送 **IOCTL \_ BTHHFP \_ 流 \_ 打开** 和 **ioctl \_ BTHHFP \_ 流 \_ 关闭**，音频驱动程序可以使用简单的引用计数机制来跟踪需要 SCO 流通道的 pin 的数目。 当引用计数从0更改为1时，音频驱动程序会打开并关闭 SCO 流通道。

在 **IOCTL \_ BTHHFP \_ 流 \_ 打开**的情况下，HFP 驱动程序会请求 sco 通道（如果尚未打开），并使用 sco 请求的结果来完成请求。 在 **IOCTL \_ BTHHFP \_ 流上 \_ 关闭** HFP 驱动程序请求 SCO 通道断开连接（如果有）。

## <a name="span-idremote_sco_connect_and_disconnectspanspan-idremote_sco_connect_and_disconnectspanspan-idremote_sco_connect_and_disconnectspanremote-sco-connect-and-disconnect"></a><span id="Remote_SCO_connect_and_disconnect"></span><span id="remote_sco_connect_and_disconnect"></span><span id="REMOTE_SCO_CONNECT_AND_DISCONNECT"></span>远程 SCO 连接和断开连接


在远程 SCO 断开连接上，如果流通道已关闭，HFP 驱动程序将不执行任何操作。 如果打开流通道，HFP 驱动程序将启动重新连接计时器。 当计时器过期时，如果 SCO 仍断开连接并且流通道仍处于打开状态，则驱动程序将请求 SCO 通道。 请注意，当 SCO 断开连接时，不会通过无线传输音频数据，因此在这段时间内音频会出现间隙。 如果 SCO 请求失败，则 HFP 驱动程序将通过完成任何调用的 [**IOCTL \_ BTHHFP \_ 流 \_ 获取 \_ 状态 \_ 更新**](/windows-hardware/drivers/ddi/bthhfpddi/ni-bthhfpddi-ioctl_bthhfp_stream_get_status_update)来向音频驱动程序发送流通道状态更改。 这应该很少见，因为远程 SCO 断开连接通常与请求将电话音频传输到音频网关的 HF 设备相关联。 音频驱动程序应将这种情况视为中间流错误情况。

此过程允许 VoIP 应用程序从 CallButtons API 接收音频传输回拨，并在 HFP 终结点上完全释放其音频资源，而不是导致流式处理错误。

在远程 SCO 连接上，如果流通道为打开状态，则驱动程序只接受连接。 如果流通道已关闭，则 HFP 驱动程序会接受连接，并且还会启动断开连接计时器。 当断开连接计时器过期时，如果 SCO 仍处于连接状态并且流通道仍处于关闭状态，则驱动程序将中断 SCO 连接。

此过程允许 VoIP 应用程序从 CallButtons API 接收音频传输回拨，并在 HFP 终结点上建立音频资源，而无需提前拒绝或关闭 SCO 连接。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[操作理论](theory-of-operation.md)