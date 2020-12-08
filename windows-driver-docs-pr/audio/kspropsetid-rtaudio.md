---
title: KSPROPSETID \_ RTAudio
description: KSPROPSETID \_ RTAudio
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c8e2d43a3c4cfaa76e527e5868743a13f69559a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801081"
---
# <a name="kspropsetid_rtaudio"></a>KSPROPSETID \_ RTAudio


`KSPROPSETID_RTAudio`属性集指定 WaveRT 音频设备的属性。 Windows Vista 和更高版本的 Windows 操作系统中支持这些属性。

在下面的属性定义中，属性为 "仅获取"，目标为 pin：

-   此属性集中的所有属性都支持从客户端 **获取** 属性请求，但不能 **设置** 属性请求。

-   对于此集合中的所有属性，客户端发送属性请求的目标是一个 pin 实例。 另一方面， (其他 KS 属性集支持筛选器实例的属性。 ) 

`KSPROPSETID_RTAudio`属性集包含以下属性：

[**KSPROPERTY \_ RTAUDIO \_ 缓冲区**](ksproperty-rtaudio-buffer.md)

[**\_ \_ \_ 带有通知的 KSPROPERTY RTAUDIO 缓冲区 \_**](ksproperty-rtaudio-buffer-with-notification.md)

[**KSPROPERTY \_ RTAUDIO \_ CLOCKREGISTER**](ksproperty-rtaudio-clockregister.md)

[**KSPROPERTY \_ RTAUDIO \_ GETREADPACKET**](ksproperty-rtaudio-getreadpacket.md)

[**KSPROPERTY \_ RTAUDIO \_ HWLATENCY**](ksproperty-rtaudio-hwlatency.md)

[**KSPROPERTY \_ RTAUDIO \_ PACKETCOUNT**](ksproperty-rtaudio-packetcount.md)

[**KSPROPERTY \_ RTAUDIO \_ POSITIONREGISTER**](ksproperty-rtaudio-positionregister.md)

[**KSPROPERTY \_ RTAUDIO \_ 演示 \_ 位置**](ksproperty-rtaudio-presentation-position.md)

[**KSPROPERTY \_ RTAUDIO \_ 查询 \_ 通知 \_ 支持**](ksproperty-rtaudio-query-notification-support.md)

[**KSPROPERTY \_ RTAUDIO \_ 注册 \_ 通知 \_ 事件**](ksproperty-rtaudio-register-notification-event.md)

[**KSPROPERTY \_ RTAUDIO \_ SETWRITEPACKET**](ksproperty-rtaudio-setwritepacket.md)

[**KSPROPERTY \_ RTAUDIO \_ 注销 \_ 通知 \_ 事件**](ksproperty-rtaudio-unregister-notification-event.md)

 

 





