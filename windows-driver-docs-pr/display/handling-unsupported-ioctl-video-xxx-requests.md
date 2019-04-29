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
ms.openlocfilehash: 9fcd563a2b3529fb78ecfd7d70e18602769b7cc4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353908"
---
# <a name="handling-unsupported-ioctlvideoxxx-requests"></a>处理不受支持的 IOCTL\_视频\_XXX 请求


## <span id="ddk_handling_unsupported_ioctl_video_xxx_requests_gg"></span><span id="DDK_HANDLING_UNSUPPORTED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


每个[ *HwVidStartIO* ](https://msdn.microsoft.com/library/windows/hardware/ff567367)函数还必须处理接收不受支持 IOCTL\_视频\_*XXX*，按如下所示：

1.  设置输入 VRP 的**状态**字段错误\_无效\_函数。

2.  设置输入 VRP 的**信息**字段为零。

3.  返回 **，则返回 TRUE**以指示处理请求。

请参阅[**视频\_请求\_数据包**](https://msdn.microsoft.com/library/windows/hardware/ff570547)并[**状态\_阻止**](https://msdn.microsoft.com/library/windows/hardware/ff569732)结构更多详细信息。

 

 





