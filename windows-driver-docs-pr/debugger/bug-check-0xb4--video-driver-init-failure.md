---
title: Bug 检查 0xB4 VIDEO_DRIVER_INIT_FAILURE
description: VIDEO_DRIVER_INIT_FAILURE bug 检查具有 0x000000B4 值。 这表示 Windows 无法进入图形模式。
ms.assetid: 37c2d07d-f351-42d0-ba88-9b9a2a3d19f8
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
ms.openlocfilehash: f045d32e3b6d06d1f407e840138b981a2aa72604
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577406"
---
# <a name="bug-check-0xb4-videodriverinitfailure"></a>Bug 检查 0xB4：视频\_驱动程序\_INIT\_失败


视频\_驱动程序\_INIT\_故障错误检查的值为 0x000000B4。 这表示 Windows 无法进入图形模式。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="videodriverinitfailure-parameters"></a>视频\_驱动程序\_INIT\_失败参数


无

<a name="cause"></a>原因
-----

系统无法进入图形模式，因为没有显示器驱动程序已启动。

这通常发生在任何微型端口驱动程序不都能够成功加载。

 

 




