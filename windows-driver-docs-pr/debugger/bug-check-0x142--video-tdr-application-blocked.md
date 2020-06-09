---
title: Bug 检查 0x142 VIDEO_TDR_APPLICATION_BLOCKED
description: VIDEO_TDR_APPLICATION_BLOCKED bug 检查的值为0x00000142。 这表明应用程序被阻止访问图形硬件。
ms.assetid: B97FCA51-C368-4144-A364-50135A8DE836
keywords:
- Bug 检查 0x142 VIDEO_TDR_APPLICATION_BLOCKED
- VIDEO_TDR_APPLICATION_BLOCKED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- VIDEO_TDR_APPLICATION_BLOCKED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 513401c67dfdb002eabb2df4df0da49bf5bbf967
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534656"
---
# <a name="bug-check-0x142-video_tdr_application_blocked"></a>Bug 检查0x142：视频 \_ TDR \_ 应用程序已 \_ 阻止


视频 \_ TDR \_ 应用程序 \_ 阻止 bug 检查的值为0x00000142。 这表明应用程序被阻止访问图形硬件。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="video_tdr_application_blocked-parameters"></a>视频 \_ TDR \_ 应用程序 \_ 阻止参数


| 参数 | 说明                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | 指向内部 TDR 恢复上下文（TDR \_ 恢复上下文）的可选指针 \_ 。 |
| 2         | 指向 "负责的设备驱动程序" 模块（例如 "所有者" 标记）的指针。          |
| 3         | 辅助驱动程序特定的存储桶键。                                |
| 4         | 阻止访问 GPU 的进程的 Id。                     |

 

<a name="remarks"></a>注解
-------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，并且在确定根本原因时可能非常有用。
Tag {270A33FD-3DA6-460D-BA89-3C1BAE21E39B} 的辅助数据包含其他 TDR 相关数据。 使用[**. enumtag （枚举辅助回调数据）**](-enumtag--enumerate-secondary-callback-data-.md)来查看数据。
