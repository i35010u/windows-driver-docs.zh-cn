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
ms.openlocfilehash: f631919f9570959777b668543d5e587afd27cab7
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534658"
---
# <a name="bug-check-0x141-video_engine_timeout_detected"></a>Bug 检查0x141： \_ \_ 检测到视频引擎超时 \_


\_检测到的视频引擎 \_ 超时 \_ bug 检查的值为0x00000141。 这表明其中一个显示引擎无法及时响应。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="video_engine_timeout_detected-parameters"></a>\_ \_ 检测到视频引擎超时 \_ 参数


| 参数 | 说明                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | 指向内部 TDR 恢复上下文（TDR \_ 恢复上下文）的可选指针 \_ 。 |
| 2         | 指向 "负责的设备驱动程序" 模块（例如 "所有者" 标记）的指针。          |
| 3         | 辅助驱动程序特定的存储桶键。                                |
| 4         | 可选的内部上下文相关数据。                                   |

 

<a name="remarks"></a>注解
-------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
Tag {270A33FD-3DA6-460D-BA89-3C1BAE21E39B} 的辅助数据包含其他 TDR 相关数据。 使用[**enumtag**](-enumtag--enumerate-secondary-callback-data-.md)查看数据。

 

 




