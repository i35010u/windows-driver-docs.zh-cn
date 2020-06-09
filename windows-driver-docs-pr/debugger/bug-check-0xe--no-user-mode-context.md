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
ms.openlocfilehash: da67bd6925996195cf3ec74ed7a94cf1f3523ce2
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534524"
---
# <a name="bug-check-0xe-no_user_mode_context"></a>Bug 检查0xE：无 \_ 用户 \_ 模式 \_ 上下文

无 \_ 用户 \_ 模式 \_ 上下文 bug 检查的值为0x0000000E。

在启动系统线程的过程中，如果控件从初始线程过程返回，将发生 bug 检查。

> [!IMPORTANT]
> 本主题适用于程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。

## <a name="resolution"></a>解决方法
[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
