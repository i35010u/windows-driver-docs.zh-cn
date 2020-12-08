---
title: Bug 检查 0x141 VIDEO_ENGINE_TIMEOUT_DETECTED
description: VIDEO_ENGINE_TIMEOUT_DETECTED bug 检查的值为0x00000141。 这表明其中一个显示引擎无法及时响应。
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
ms.openlocfilehash: 8e3fea711330f68ed798af34c31ecb26ed676ca6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824299"
---
# <a name="bug-check-0x141-video_engine_timeout_detected"></a>Bug 检查0x141： \_ \_ 检测到视频引擎超时 \_


\_检测到的视频引擎 \_ 超时 \_ bug 检查的值为0x00000141。 这表明其中一个显示引擎无法及时响应。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="video_engine_timeout_detected-parameters"></a>\_ \_ 检测到视频引擎超时 \_ 参数


| 参数 | 描述                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | 指向内部 TDR 恢复上下文的可选指针， (TDR \_ 恢复 \_ 上下文) 。 |
| 2         | 指向 "负责的设备驱动程序" 模块 (例如所有者标记) 。          |
| 3         | 辅助驱动程序特定的存储桶键。                                |
| 4         | 可选的内部上下文相关数据。                                   |

 

<a name="remarks"></a>备注
-------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
Tag {270A33FD-3DA6-460D-BA89-3C1BAE21E39B} 的辅助数据包含其他 TDR 相关数据。 使用 [**enumtag**](-enumtag--enumerate-secondary-callback-data-.md) 查看数据。

 

 




