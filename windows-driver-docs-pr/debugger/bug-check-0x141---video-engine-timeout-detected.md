---
title: Bug 检查 0x141 VIDEO_ENGINE_TIMEOUT_DETECTED
description: VIDEO_ENGINE_TIMEOUT_DETECTED bug 检查的值为0x00000141。 这表明其中一个显示引擎无法及时响应。
ms.assetid: 0912495D-DE6D-4064-BD66-DA6145889821
keywords:
- Bug 检查 0x141 VIDEO_ENGINE_TIMEOUT_DETECTED
- VIDEO_ENGINE_TIMEOUT_DETECTED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_ENGINE_TIMEOUT_DETECTED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d5bc5812549e86480da6d905d8364601c03b7133
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038101"
---
# <a name="bug-check-0x141-video_engine_timeout_detected"></a>Bug 检查 0x141：VIDEO @ NO__T-0ENGINE @ NO__T-1TIMEOUT @ NO__T-2DETECTED


视频 @ no__t-0ENGINE @ no__t-1TIMEOUT @ no__t-2DETECTED bug 检查的值为0x00000141。 这表明其中一个显示引擎无法及时响应。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="video_engine_timeout_detected-parameters"></a>VIDEO @ no__t-0ENGINE @ no__t-1TIMEOUT @ no__t-2DETECTED 参数


| 参数 | 描述                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | 指向内部 TDR 恢复上下文的可选指针（TDR @ no__t-0RECOVERY @ no__t-1CONTEXT）。 |
| 2         | 指向 "负责的设备驱动程序" 模块（例如 "所有者" 标记）的指针。          |
| 3         | 辅助驱动程序特定的存储桶键。                                |
| 4         | 可选的内部上下文相关数据。                                   |

 

<a name="remarks"></a>备注
-------

[ **！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
Tag {270A33FD-3DA6-460D-BA89-3C1BAE21E39B} 的辅助数据包含其他 TDR 相关数据。 使用[**enumtag**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-enumtag--enumerate-secondary-callback-data-)查看数据。

 

 




