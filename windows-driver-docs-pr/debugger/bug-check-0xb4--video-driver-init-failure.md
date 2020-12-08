---
title: Bug 检查 0xB4 VIDEO_DRIVER_INIT_FAILURE
description: VIDEO_DRIVER_INIT_FAILURE bug 检查的值为0x000000B4。 这表明 Windows 无法进入图形模式。
keywords:
- Bug 检查 0xB4 VIDEO_DRIVER_INIT_FAILURE
- VIDEO_DRIVER_INIT_FAILURE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_DRIVER_INIT_FAILURE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f77cf43fd1a2479544180d0fb1a12a35255d6628
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832845"
---
# <a name="bug-check-0xb4-video_driver_init_failure"></a>Bug 检查0xB4：视频 \_ 驱动程序 \_ 初始化 \_ 失败


视频 \_ 驱动程序 \_ 初始化 \_ 失败 bug 检查的值为0x000000B4。 这表明 Windows 无法进入图形模式。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="video_driver_init_failure-parameters"></a>视频 \_ 驱动程序 \_ 初始化 \_ 失败参数


无

<a name="cause"></a>原因
-----

系统无法进入图形模式，因为没有显示驱动程序可以启动。

如果没有视频微型端口驱动程序无法成功加载，通常会发生这种情况。

 

 




