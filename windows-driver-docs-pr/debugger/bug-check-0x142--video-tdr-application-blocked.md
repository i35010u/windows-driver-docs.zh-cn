---
title: Bug 检查 0x142 VIDEO_TDR_APPLICATION_BLOCKED
description: VIDEO_TDR_APPLICATION_BLOCKED bug 检查的值为0x00000142。 这表明应用程序被阻止访问图形硬件。
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
ms.openlocfilehash: 85aab19c8d9aab39e099306fa6a46adffaf2dfe0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824293"
---
# <a name="bug-check-0x142-video_tdr_application_blocked"></a>Bug 检查0x142：视频 \_ TDR \_ 应用程序已 \_ 阻止


视频 \_ TDR \_ 应用程序 \_ 阻止 bug 检查的值为0x00000142。 这表明应用程序被阻止访问图形硬件。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="video_tdr_application_blocked-parameters"></a>视频 \_ TDR \_ 应用程序 \_ 阻止参数


| 参数 | 描述                                                                 |
|-----------|-----------------------------------------------------------------------------|
| 1         | 指向内部 TDR 恢复上下文的可选指针， (TDR \_ 恢复 \_ 上下文) 。 |
| 2         | 指向 "负责的设备驱动程序" 模块 (例如所有者标记) 。          |
| 3         | 辅助驱动程序特定的存储桶键。                                |
| 4         | 阻止访问 GPU 的进程的 Id。                     |

 

<a name="remarks"></a>备注
-------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，并且在确定根本原因时可能非常有用。
Tag {270A33FD-3DA6-460D-BA89-3C1BAE21E39B} 的辅助数据包含其他 TDR 相关数据。 使用 [**. enumtag (枚举辅助回叫数据)**](-enumtag--enumerate-secondary-callback-data-.md) 以查看数据。
