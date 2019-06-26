---
title: 处理不受支持的 IOCTL_VIDEO_XXX 请求
description: 处理不受支持的 IOCTL_VIDEO_XXX 请求
ms.assetid: e3a96cc2-bb7f-4060-bf71-d8a63b918329
keywords:
- 微型端口驱动程序 WDK Windows 2000 中，处理请求
- 请求处理 WDK 微型端口
- 不支持的 IOCTL_VIDEO_XXX 请求 WDK 微型端口
- IOCTL_VIDEO_XXX 请求 WDK 微型端口
- I/O WDK 微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b9ae27c740f26e72a28d9a0f772dd0cb27cee0d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67369827"
---
# <a name="handling-unsupported-ioctlvideoxxx-requests"></a>处理不受支持的 IOCTL\_视频\_XXX 请求


## <span id="ddk_handling_unsupported_ioctl_video_xxx_requests_gg"></span><span id="DDK_HANDLING_UNSUPPORTED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


每个[ *HwVidStartIO* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/nc-video-pvideo_hw_start_io)函数还必须处理接收不受支持 IOCTL\_视频\_*XXX*，按如下所示：

1.  设置输入 VRP 的**状态**字段错误\_无效\_函数。

2.  设置输入 VRP 的**信息**字段为零。

3.  返回 **，则返回 TRUE**以指示处理请求。

请参阅[**视频\_请求\_数据包**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_video_request_packet)并[**状态\_阻止**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/video/ns-video-_status_block)结构更多详细信息。

 

 





