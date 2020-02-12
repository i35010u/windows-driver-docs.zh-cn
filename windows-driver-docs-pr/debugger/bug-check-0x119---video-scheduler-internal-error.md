---
title: Bug 检查 0x119 VIDEO_SCHEDULER_INTERNAL_ERROR
description: VIDEO_SCHEDULER_INTERNAL_ERROR bug 检查的值为0x00000119。 这表示视频计划程序检测到严重冲突。
ms.assetid: dfffdd70-c519-4e39-a604-a0ba2217093b
keywords:
- Bug 检查 0x119 VIDEO_SCHEDULER_INTERNAL_ERROR
- VIDEO_SCHEDULER_INTERNAL_ERROR
ms.date: 02/07/2020
topic_type:
- apiref
api_name:
- VIDEO_SCHEDULER_INTERNAL_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 27b864db5982677a361f6eb57ca6d3277200f074
ms.sourcegitcommit: 8fce8b22c7437f0aa322c40625d5163e8812ea01
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2020
ms.locfileid: "77146507"
---
# <a name="bug-check-0x119-video_scheduler_internal_error"></a>Bug 检查0x119：视频\_计划程序\_内部\_错误

视频\_计划程序\_内部\_错误 bug 检查的值为0x00000119。 这表示视频计划程序检测到严重冲突。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

## <a name="video_scheduler_internal_error-parameters"></a>视频\_计划程序\_内部\_错误参数

参数1是唯一相关的参数，用于标识完全冲突。

| 参数 1 | 错误的原因                                       |
|-----------|--------------------------------------------------------|
|0x1|驱动程序报告了无效的防护 ID。 |
|0x2| 提交命令时驱动程序失败。|
|0x3|驱动程序在修补命令缓冲区时失败。 |
|0x4| 驱动程序报告了无效的翻转功能。|
|0x5| 驱动程序未通过系统或寻呼命令。|
|0x400| 这是一个内部操作系统状态错误，通常是由于内存损坏或硬件错误造成的。|
|0xE00 | 操作系统耗尽了内存，无法用于预分配的数据包来处理被动翻转请求。|
|0x1000| 这是一个内部操作系统状态错误，通常是由于内存损坏或硬件错误造成的。|
|0x10000| 这是一个内部操作系统状态错误，通常是由于内存损坏或硬件错误造成的。|

## <a name="resolution"></a>分辨率

[ **！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

如果！分析输出中列出的错误模块是视频驱动程序，请调查供应商是否有更新可供该视频驱动程序使用。

有关详细信息，请参阅：

[处理命令和 DMA 缓冲区](https://docs.microsoft.com/windows-hardware/drivers/display/handling-command-and-dma-buffers)

[提交命令缓冲区](https://docs.microsoft.com/windows-hardware/drivers/display/submitting-a-command-buffer)

[提供防护标识符](https://docs.microsoft.com/windows-hardware/drivers/display/supplying-fence-identifiers)

[GPU 计划程序类](https://docs.microsoft.com/windows-hardware/drivers/display/gpu-scheduler-class)

[视频内存的直接翻转](https://docs.microsoft.com/windows-hardware/drivers/display/direct-flip-of-video-memory)