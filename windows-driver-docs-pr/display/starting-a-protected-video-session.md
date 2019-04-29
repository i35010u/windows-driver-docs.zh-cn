---
title: 启动受保护的视频会话
description: 启动受保护的视频会话
ms.assetid: c92f2d1a-ac15-49d4-858b-ff207ff4810c
keywords:
- 复制保护 WDK COPP 启动受保护的视频会话
- 视频复制保护 WDK COPP 启动受保护的视频会话
- COPP WDK DirectX VA，启动受保护的视频课程
- 受保护视频 WDK COPP 启动会话
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 15ecca5754a3df8e0857d69de15de968fde21e59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376015"
---
# <a name="starting-a-protected-video-session"></a>启动受保护的视频会话


## <span id="ddk_starting_a_protected_video_session_gg"></span><span id="DDK_STARTING_A_PROTECTED_VIDEO_SESSION_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。**

若要启动受保护的视频课程，VMR 应启动特定的顺序在 DirectX VA COPP 设备上的操作。 如果未遵循此顺序，微型端口驱动程序应返回错误代码 E\_意外的。 微型端口驱动程序可以确定正确的操作顺序后到 COPP 设备分配一个唯一的设备状态常量时执行操作，然后在执行后续之前验证设备状态常量操作。

若要启动受保护的视频课程，应该对按以下顺序 COPP 设备函数进行调用：

1.  [ *COPPOpenVideoSession* ](https://msdn.microsoft.com/library/windows/hardware/ff539650)函数以初始化 COPP 设备。 再返回，该驱动程序应将设备状态常量设置为 COPP\_打开。

2.  [ *COPPGetCertificateLength* ](https://msdn.microsoft.com/library/windows/hardware/ff539644)函数以检索大小 （字节） 使用图形硬件的证书。 该驱动程序应首先验证设备状态常量当前设置为 COPP\_打开。 如果它不是，则驱动程序应返回 E\_意外的。 再返回，该驱动程序应将设备状态常量设置为 COPP\_CERT\_长度\_返回。

3.  [ *COPPKeyExchange* ](https://msdn.microsoft.com/library/windows/hardware/ff539646)函数以检索用于图形硬件的数字证书。 该驱动程序应首先验证设备状态常量当前设置为 COPP\_CERT\_长度\_返回。 如果它不是，则驱动程序应返回 E\_意外的。 再返回，该驱动程序应将设备状态常量设置为 COPP\_密钥\_EXCHANGED。

4.  [ *COPPSequenceStart* ](https://msdn.microsoft.com/library/windows/hardware/ff540421)函数将视频会话设置为受保护模式。 该驱动程序应首先验证设备状态常量当前设置为 COPP\_密钥\_EXCHANGED。 如果它不是，则驱动程序应返回 E\_意外的。 再返回，该驱动程序应将设备状态常量设置为 COPP\_会话\_活动状态以显示视频会话是在受保护模式下。

视频会话设置为受保护模式后，可以处理的微型端口驱动程序[COPP 命令](copp-commands.md)，并且请求[COPP 状态](copp-status.md)，并将传递[COPP 状态事件](copp-status-events.md)。

 

 





