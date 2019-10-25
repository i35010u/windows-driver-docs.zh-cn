---
title: Bug 检查回调的视频端口驱动程序支持
description: Bug 检查回调的视频端口驱动程序支持
ms.assetid: 181fd4f2-feed-4759-80a7-aec97b9094b3
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，bug 检查回调
- bug 检查回调 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51a7080ea6c95b11ad1480197b6c0eba677f2522
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72829185"
---
# <a name="video-port-driver-support-for-bug-check-callbacks"></a>Bug 检查回调的视频端口驱动程序支持


## <span id="ddk_video_port_driver_support_for_bug_check_callbacks_gg"></span><span id="DDK_VIDEO_PORT_DRIVER_SUPPORT_FOR_BUG_CHECK_CALLBACKS_GG"></span>


在 Windows XP SP1 和更高版本中，视频微型端口驱动程序可以实现并注册[**HwVidBugcheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_bugcheck_callback)，这是一个函数，当[**Bug 检查0xEA （线程\_停滞\_\_设备\_驱动程序）** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/bug-check-0xea--thread-stuck-in-device-driver)时，系统会调用此函数。 *HwVidBugcheckCallback*可以将其自己的数据追加到一个转储文件中，驱动程序开发人员可以使用它来诊断其驱动程序中的问题。

有关注册*HwVidBugcheckCallback*的信息，请参阅以下主题：

[单独注册的视频微型端口驱动程序函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/index)

[**VideoPortRegisterBugcheckCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nf-video-videoportregisterbugcheckcallback)

 

 





