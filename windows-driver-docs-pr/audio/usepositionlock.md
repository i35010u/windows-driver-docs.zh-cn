---
title: UsePositionLock
description: UsePositionLock 注册表值更改 PortCls 如何序列化其 I/O。
ms.assetid: AD5AF873-4129-4C82-B251-0469CF6149E9
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76e82ddeb510ae5909c5db1ea60ea86e809eff25
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354158"
---
# <a name="usepositionlock"></a>UsePositionLock


*UsePositionLock*注册表值发生更改时如何 PortCls 序列化其 I/O。 启用此设置可能会有所帮助如果音频驱动程序存在问题归因于全局设备锁定该 portcls 将使用序列化。 请注意，当*UsePositionLock*是启用，它将由音频驱动程序应用下面列出的回调和其他属性的回调之间的任何序列化 （如果需要）。 默认情况下不启用此标志。 之前将其打开，请务必查看驱动程序进行任何驱动程序的回调之间的争用条件。

使用以下 INF 设置来启用此行为。

```inf
 
[MyAudioDevice.AddReg]
HKR, DispatchSettings, UsePositionLock, 3, 01, 00, 00, 00
```

此 INF 设置创建以下注册表值。 媒体 {4d36e96c-e325-11ce-bfc1-08002be10318} 的 GUID 和&lt;实例\#&gt;音频设备的，使用注册表项路径中。

```text
\HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Class\{4d36e96c-e325-11ce-bfc1-08002be10318}\<instance#>\DispatchSettings\UsePositionLock 
```

当此值设置为 1 或更高版本时，portcls 使用流式处理的位置锁序列化为下面列出的回调。 如果不存在或设置为零，默认行为是使用全局设备锁定。 此值是读取第一次添加设备。

*UsePositionLock* WaveRT 上仅支持设置和拓扑筛选器。 Portcls 读取此注册表值的设备添加时间和设置仍然存在，直到删除功能的设备对象 (FDO)。

如果 portcls 检测到已启用了此标志，它不会序列化与全局设备锁定的以下属性。

-   {KSPROPSETID\_RtAudio， [ **KSPROPERTY\_RTAUDIO\_GETREADPACKET**](ksproperty-rtaudio-getreadpacket.md)}

-   {KSPROPSETID\_RtAudio， [ **KSPROPERTY\_RTAUDIO\_SETWRITEPACKET**](ksproperty-rtaudio-setwritepacket.md)}

-   {KSPROPSETID\_RtAudio， [ **KSPROPERTY\_RTAUDIO\_演示文稿\_位置**](ksproperty-rtaudio-presentation-position.md)}

-   {KSPROPSETID\_RtAudio， [ **KSPROPERTY\_RTAUDIO\_PACKETCOUNT**](ksproperty-rtaudio-packetcount.md)}

-   {KSPROPSETID\_Audio,[**KSPROPERTY\_AUDIO\_POSITION**](ksproperty-audio-position.md)}

-   {KSPROPSETID\_音频[ **KSPROPERTY\_音频\_POSITIONEX**](ksproperty-audio-positionex.md)}

这意味着以下微型端口的回调不会序列化与其他属性请求 （包括设置状态的请求）。

-   [**IMiniportWaveRTInputStream::GetReadPacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertinputstream-getreadpacket)

-   [**IMiniportWaveRTOutputStream::SetWritePacket**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertoutputstream-setwritepacket)

-   [**IMiniportWaveRTOutputStream::GetOutputStreamPresentationPosition**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertoutputstream-getoutputstreampresentationposition)

-   [**IMiniportWaveRTOutputStream::GetPacketCount**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/portcls/nf-portcls-iminiportwavertoutputstream-getpacketcount)

-   [**IMiniportWaveRTStream::GetPosition**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff536749(v=vs.85))

 

 





