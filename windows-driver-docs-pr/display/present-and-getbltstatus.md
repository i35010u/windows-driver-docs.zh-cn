---
title: 呈现和 GetBltStatus
description: 呈现和 GetBltStatus
ms.assetid: 76fd88df-18a9-4f00-834d-6683788fc2f6
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示，演示
- 演示文稿 WDK DirectX 8。0
- 呈现结果可见 WDK DirectX 8。0
- 可见结果 WDK DirectX 8。0
- DdGetBltStatus
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 41f5db3590ebbb68ddaf7d55dbedab9d74cffcf3
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066456"
---
# <a name="present-and-getbltstatus"></a>呈现和 GetBltStatus


## <span id="ddk_present_and_getbltstatus_gg"></span><span id="DDK_PRESENT_AND_GETBLTSTATUS_GG"></span>


对于 DX8，运行时不再调用涉及系统内存表面的 blts 上的 [*DdGetBltStatus*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getbltstatus) 。 这始终是 Windows 2000 上的行为。 结果是，不能再从系统内存表面进行异步 DMA。 DX8 驱动程序不应单独页面锁定系统内存表面，视频内存传输的系统内存应是同步的。

 

