---
title: Bug 检查回调的视频端口驱动程序支持
description: Bug 检查回调的视频端口驱动程序支持
ms.assetid: 181fd4f2-feed-4759-80a7-aec97b9094b3
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，bug 检查回调
- bug 检查回调 WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a7e707321033aac2e69efa04f2efb738e2394ed6
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063440"
---
# <a name="video-port-driver-support-for-bug-check-callbacks"></a>Bug 检查回调的视频端口驱动程序支持


## <span id="ddk_video_port_driver_support_for_bug_check_callbacks_gg"></span><span id="DDK_VIDEO_PORT_DRIVER_SUPPORT_FOR_BUG_CHECK_CALLBACKS_GG"></span>


在 Windows XP SP1 和更高版本中，视频微型端口驱动程序可以实现并注册 [**HwVidBugcheckCallback**](/windows-hardware/drivers/ddi/video/nc-video-pvideo_bugcheck_callback)，这是一个函数，当 [**Bug 检查 0xEA (线程 \_ 停滞 \_ 在 \_ 设备 \_ 驱动程序中 **](../debugger/bug-check-0xea--thread-stuck-in-device-driver.md) 时，系统会调用该函数) 出现。 *HwVidBugcheckCallback* 可以将其自己的数据追加到一个转储文件中，驱动程序开发人员可以使用它来诊断其驱动程序中的问题。

有关注册 *HwVidBugcheckCallback*的信息，请参阅以下主题：

[单独注册的视频微型端口驱动程序函数](/windows-hardware/drivers/ddi/index)

[**VideoPortRegisterBugcheckCallback**](/windows-hardware/drivers/ddi/video/nf-video-videoportregisterbugcheckcallback)

 

