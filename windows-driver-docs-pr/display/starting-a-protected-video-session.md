---
title: 启动受保护的视频会话
description: 启动受保护的视频会话
keywords:
- 复制保护 WDK COPP，启动受保护的视频会话
- 视频复制保护 WDK COPP，启动受保护的视频会话
- COPP WDK DirectX VA，启动受保护的视频会话
- 受保护的视频 WDK COPP，启动会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3dc0be29f5ab8cc136d4051e4efcd8b4d75b32f8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820811"
---
# <a name="starting-a-protected-video-session"></a>启动受保护的视频会话


## <span id="ddk_starting_a_protected_video_session_gg"></span><span id="DDK_STARTING_A_PROTECTED_VIDEO_SESSION_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

若要启动受保护的视频会话，VMR 应按特定顺序在 DirectX VA COPP 设备上启动操作。 如果未遵循此顺序，则视频微型端口驱动程序应返回意外错误代码 E \_ 。 在执行操作时，视频微型端口驱动程序可以确定正确的操作顺序，并在执行操作时将唯一的设备状态常数分配给 COPP 设备，然后在执行后续操作之前验证设备状态常量。

若要启动受保护的视频会话，应按以下顺序对 COPP 设备的函数进行调用：

1.  用于初始化 COPP 设备的 [*COPPOpenVideoSession*](./coppopenvideosession.md) 函数。 在返回之前，驱动程序应将设备状态常量设置为打开的 COPP \_ 。

2.  用于检索图形硬件使用的证书大小（以字节为单位）的 [*COPPGetCertificateLength*](./coppgetcertificatelength.md) 函数。 驱动程序应首先验证设备状态常量当前是否设置为 "COPP 已 \_ 打开"。 如果不是，则驱动程序应返回 E \_ 。 在返回之前，驱动程序应将设备状态常量设置为返回的 COPP \_ CERT \_ LENGTH \_ 。

3.  用于检索图形硬件使用的数字证书的 [*COPPKeyExchange*](./coppkeyexchange.md) 函数。 驱动程序应首先验证设备状态常量当前是否设置为返回的 COPP \_ CERT \_ LENGTH \_ 。 如果不是，则驱动程序应返回 E \_ 。 在返回之前，驱动程序应将设备状态常量设置为交换的 COPP \_ 密钥 \_ 。

4.  用于将视频会话设置为受保护模式的 [*COPPSequenceStart*](./coppsequencestart.md) 函数。 该驱动程序应该首先验证设备状态常量当前是否设置为 COPP \_ 密钥 \_ 交换。 如果不是，则驱动程序应返回 E \_ 。 在返回之前，驱动程序应将设备状态常量设置为活动的 COPP \_ 会话， \_ 以显示视频会话处于受保护模式。

视频会话设置为 "保护模式" 后，视频微型端口驱动程序可以处理 [COPP 命令](copp-commands.md) 和 [COPP 状态](copp-status.md)请求，并通过 [COPP 状态事件传递状态事件](copp-status-events.md)。

 

