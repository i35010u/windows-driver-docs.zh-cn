---
title: 报告多头视频内存
description: 报告多头视频内存
ms.assetid: 664b60f5-9e19-4dfc-8bd7-73ceccf6cbea
keywords:
- 多头硬件 WDK DirectX 9.0，内存报告
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc578c613d17d2263de361fe8509b50773ba951d
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063818"
---
# <a name="reporting-multiple-head-video-memory"></a>报告多头视频内存


## <span id="ddk_reporting_multiple_head_video_memory_gg"></span><span id="DDK_REPORTING_MULTIPLE_HEAD_VIDEO_MEMORY_GG"></span>


在多头模式下，主头必须响应对驱动程序的 [*DdGetAvailDriverMemory*](/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getavaildrivermemory) 函数的调用，就像主头是控制多个头卡的唯一头一样。 驱动程序返回的可用内存量必须包括其视频内存被 surrendered 到主 head (的任何从属标头的视频内存，即收到 *DdCreateSurface* 调用且 DDSCAPS2 \_ ADDITIONALPRIMARY 位集) 的任何从属头。

 

