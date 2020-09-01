---
title: 确定是否已附加调试器
description: 确定是否已附加调试器
ms.assetid: 78f7d90a-459c-4967-a980-3f8d6339eb77
keywords:
- 确定调试器是否已附加
- KdRefreshDebuggerNotPresent 函数
- KD_DEBUGGER_ENABLED 全局变量
- KD_DEBUGGER_NOT_PRESENT 全局变量
ms.date: 07/20/2020
ms.localizationpriority: medium
ms.openlocfilehash: 40c2c6c05aa3bea87f241ffb0ccf90b32189d896
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216734"
---
# <a name="determining-if-a-debugger-is-attached"></a>确定是否已附加调试器

内核模式代码可以通过使用以下变量和例程来确定内核调试的状态：

- [** \_ \_ 启用了 KD 调试器**](/previous-versions/ff548118(v=vs.85))的全局内核变量指示是否启用内核调试。

- [**KD \_ 调试器 \_ 不 \_ 存在**](/previous-versions/ff548125(v=vs.85))全局内核变量指示当前是否附加了内核调试器。

- [**KdRefreshDebuggerNotPresent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kdrefreshdebuggernotpresent)例程刷新 KD \_ 调试器不存在的值 \_ \_ 。