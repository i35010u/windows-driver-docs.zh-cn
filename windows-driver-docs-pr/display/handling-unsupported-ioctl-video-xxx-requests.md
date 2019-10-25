---
title: 处理不受支持的 IOCTL_VIDEO_XXX 请求
description: 处理不受支持的 IOCTL_VIDEO_XXX 请求
ms.assetid: e3a96cc2-bb7f-4060-bf71-d8a63b918329
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，处理请求
- 请求处理 WDK 视频微型端口
- 不支持的 IOCTL_VIDEO_XXX 请求 WDK 视频微型端口
- IOCTL_VIDEO_XXX 请求 WDK 视频微型端口
- I/o WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 052b6cc23759a7c3dc32755c8b76138a30f73e3f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72839656"
---
# <a name="handling-unsupported-ioctl_video_xxx-requests"></a>处理不受支持的 IOCTL\_视频\_XXX 请求


## <span id="ddk_handling_unsupported_ioctl_video_xxx_requests_gg"></span><span id="DDK_HANDLING_UNSUPPORTED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


每个[*HwVidStartIO*](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)函数还必须处理收到不受支持的 IOCTL\_视频\_*XXX*，如下所示：

1.  将输入 VRP 的**状态**字段设置为 ERROR\_无效\_函数。

2.  将输入 VRP 的**信息**字段设置为零。

3.  返回**TRUE**以指示已处理请求。

有关更多详细信息，请参阅[**视频\_请求\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet)和[**状态\_块**](https://docs.microsoft.com/windows-hardware/drivers/ddi/video/ns-video-_status_block)结构。

 

 





