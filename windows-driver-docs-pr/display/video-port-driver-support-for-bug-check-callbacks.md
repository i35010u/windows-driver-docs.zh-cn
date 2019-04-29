---
title: Bug 检查回调的视频端口驱动程序支持
description: Bug 检查回调的视频端口驱动程序支持
ms.assetid: 181fd4f2-feed-4759-80a7-aec97b9094b3
keywords:
- 微型端口驱动程序 WDK Windows 2000，bug 检查回调
- bug 检查回调 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4de71773780a510b68e0cd448c221d2be7fc522e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389609"
---
# <a name="video-port-driver-support-for-bug-check-callbacks"></a>Bug 检查回调的视频端口驱动程序支持


## <span id="ddk_video_port_driver_support_for_bug_check_callbacks_gg"></span><span id="DDK_VIDEO_PORT_DRIVER_SUPPORT_FOR_BUG_CHECK_CALLBACKS_GG"></span>


微型端口驱动程序在 Windows XP SP1 和更高版本，可实现和注册[ **HwVidBugcheckCallback**](https://msdn.microsoft.com/library/windows/hardware/ff567324)，系统调用时的函数[ **Bug 检查 0xEA （线程\_STUCK\_IN\_设备\_驱动程序)** ](https://msdn.microsoft.com/library/windows/hardware/ff560350)时发生。 *HwVidBugcheckCallback*可以将其自己的数据附加到的转储文件，驱动程序开发人员可用于诊断其驱动程序中的问题。

有关注册信息*HwVidBugcheckCallback*，请参阅以下主题：

[单独注册视频微型端口驱动程序函数](https://msdn.microsoft.com/library/windows/hardware/ff567672)

[**VideoPortRegisterBugcheckCallback**](https://msdn.microsoft.com/library/windows/hardware/ff570353)

 

 





