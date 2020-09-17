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
ms.openlocfilehash: 9cab0515b0926b3757a557a3303ff03781042523
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715156"
---
# <a name="present-and-getbltstatus"></a>呈现和 GetBltStatus


## <span id="ddk_present_and_getbltstatus_gg"></span><span id="DDK_PRESENT_AND_GETBLTSTATUS_GG"></span>


对于 DX8，运行时不再调用涉及系统内存表面的 blts 上的 [*DdGetBltStatus*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_getbltstatus) 。 这始终是 Windows 2000 上的行为。 结果是，不能再从系统内存表面进行异步 DMA。 DX8 驱动程序不应单独页面锁定系统内存表面，视频内存传输的系统内存应是同步的。

 

