---
title: Bug 检查 0xE NO_USER_MODE_CONTEXT
description: NO_USER_MODE_CONTEXT bug 检查的值为0x0000000E。此 bug 检查很少出现。
ms.assetid: 0c3b3da9-c9e6-443d-9087-9bee9aa1e41a
keywords:
- Bug 检查 0xE NO_USER_MODE_CONTEXT
- NO_USER_MODE_CONTEXT
ms.date: 06/21/2019
topic_type:
- apiref
api_name:
- NO_USER_MODE_CONTEXT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 02a3f23810eafc9b2b0e1cbcc556bd292cba0d9a
ms.sourcegitcommit: 5f22002ceaf9dccd0d761327a1bb1edce4fe94f2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/04/2019
ms.locfileid: "73567186"
---
# <a name="bug-check-0xe-no_user_mode_context"></a>Bug 检查0xE： NO\_用户\_模式\_上下文

不\_用户\_模式\_上下文 bug 检查的值为0x0000000E。

在启动系统线程的过程中，如果控件从初始线程过程返回，将发生 bug 检查。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

## <a name="resolution"></a>分辨率
[ **！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
