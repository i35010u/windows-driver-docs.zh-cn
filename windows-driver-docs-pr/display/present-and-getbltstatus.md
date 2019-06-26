---
title: 呈现和 GetBltStatus
description: 呈现和 GetBltStatus
ms.assetid: 76fd88df-18a9-4f00-834d-6683788fc2f6
keywords:
- DirectX 8.0 发行说明 WDK Windows 2000 显示、 演示文稿
- 演示文稿 WDK DirectX 8.0
- 呈现结果可见 WDK DirectX 8.0
- 可见结果 WDK DirectX 8.0
- DdGetBltStatus
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14aa4edffd07f8a48f0da46e08aaf603c4eeeb12
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371368"
---
# <a name="present-and-getbltstatus"></a>呈现和 GetBltStatus


## <span id="ddk_present_and_getbltstatus_gg"></span><span id="DDK_PRESENT_AND_GETBLTSTATUS_GG"></span>


对于 DX8 运行时不会再调用[ *DdGetBltStatus* ](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_surfcb_getbltstatus) blts 涉及系统内存图面上。 这始终是 Windows 2000 上的行为。 结果是不再可以异步 DMA 到或从系统内存图面。 DX8 驱动程序不应本身是页锁定系统内存图面和视频内存传输到系统内存应该同步。

 

 





