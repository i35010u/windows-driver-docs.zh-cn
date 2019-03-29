---
title: 确定是否已附加调试器
description: 确定是否已附加调试器
ms.assetid: 78f7d90a-459c-4967-a980-3f8d6339eb77
keywords:
- 确定是否已将调试器附加
- KdRefreshDebuggerNotPresent 函数
- KD_DEBUGGER_ENABLED 全局变量
- KD_DEBUGGER_NOT_PRESENT 全局变量
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 90e6bddc42dc2ce5b0edb4eab70a6f6c4d0c507c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566537"
---
# <a name="determining-if-a-debugger-is-attached"></a>确定是否已附加调试器


## <span id="ddk_determining_if_a_debugger_is_attached_dbg"></span><span id="DDK_DETERMINING_IF_A_DEBUGGER_IS_ATTACHED_DBG"></span>


内核模式代码可以确定的内核调试通过使用以下变量和例程的状态：

-   KD\_调试器\_已启用全局内核变量指示是否启用内核调试。

-   KD\_调试器\_不\_存在全局内核变量指示当前是否附加内核调试程序。

-   (Windows Server 2003 及更高版本)**KdRefreshDebuggerNotPresent**例程刷新 KD 的值\_调试器\_不\_存在。

有关完整文档，请参阅 Windows 驱动程序工具包。

 

 





