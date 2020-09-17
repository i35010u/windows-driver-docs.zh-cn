---
title: 报告多头视频内存
description: 报告多头视频内存
ms.assetid: 664b60f5-9e19-4dfc-8bd7-73ceccf6cbea
keywords:
- 多头硬件 WDK DirectX 9.0，内存报告
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 10d8790e73b0fa5032c6806d90b11dacfa2141f9
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90716004"
---
# <a name="reporting-multiple-head-video-memory"></a>报告多头视频内存


## <span id="ddk_reporting_multiple_head_video_memory_gg"></span><span id="DDK_REPORTING_MULTIPLE_HEAD_VIDEO_MEMORY_GG"></span>


在多头模式下，主头必须响应对驱动程序的 [*DdGetAvailDriverMemory*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_getavaildrivermemory) 函数的调用，就像主头是控制多个头卡的唯一头一样。 驱动程序返回的可用内存量必须包括其视频内存被 surrendered 到主 head (的任何从属标头的视频内存，即收到 *DdCreateSurface* 调用且 DDSCAPS2 \_ ADDITIONALPRIMARY 位集) 的任何从属头。

 

