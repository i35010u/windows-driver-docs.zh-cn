---
title: 释放上下文
description: 释放上下文
keywords:
- 上下文 WDK 文件系统微筛选器，释放
- 释放上下文
ms.date: 01/22/2021
ms.localizationpriority: medium
ms.openlocfilehash: ea8c18cf51140ceac9b84af2259fbcb5b8619ddd
ms.sourcegitcommit: 204ed37ede1cd462ef6f6c9211a223fd304da4a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "99502034"
---
# <a name="freeing-contexts"></a>释放上下文

上下文在被 [删除](deleting-contexts.md) 后会被释放，并且对它的所有未完成引用都已 [释放](releasing-contexts.md)。

此规则有一个例外：如果上下文已 [创建](creating-contexts.md) 但尚未 [设置](setting-contexts.md)，则无需删除它。 它在其引用计数达到零时被释放。 请参阅 [释放上下文](releasing-contexts.md)中的代码示例。

当微筛选器 [注册其上下文类型](registering-context-types.md)时，每个上下文定义可以选择性地包含要在释放上下文之前调用的上下文清理回调例程。 有关详细信息，请参阅 [**PFLT_CONTEXT_CLEANUP_CALLBACK**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_context_cleanup_callback)。
