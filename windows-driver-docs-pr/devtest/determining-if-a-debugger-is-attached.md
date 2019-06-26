---
title: 确定是否已附加调试器
description: 确定是否已附加调试器
ms.assetid: b40482c4-7186-4632-b1d9-3c91a415b7c8
keywords:
- 调试代码 WDK 时，附加调试器
- 附加的调试器 WDK
- 状态信息 WDK 调试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5bb9b33f6ee3ce0571adba5e75ec593e37b3624
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371409"
---
# <a name="determining-if-a-debugger-is-attached"></a>确定是否已附加调试器


## <span id="ddk_determining_if_a_debugger_is_attached_tools"></span><span id="DDK_DETERMINING_IF_A_DEBUGGER_IS_ATTACHED_TOOLS"></span>


您可能想要使特定的操作，与您的驱动程序，如果当前附加内核调试程序。

若要确定的内核调试状态，以下变量和例程很有用：

-   (Microsoft Windows XP 及更高版本)[ **KD\_调试器\_已启用**](https://docs.microsoft.com/previous-versions/ff548118(v=vs.85))全局内核变量指示是否启用内核调试。

-   (Windows XP 及更高版本)[ **KD\_调试器\_不\_存在**](https://docs.microsoft.com/previous-versions/ff548125(v=vs.85))全局内核变量指示当前是否附加内核调试程序。

-   (Microsoft Windows Server 2003 及更高版本)[ **KdRefreshDebuggerNotPresent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-kdrefreshdebuggernotpresent)例程刷新 KD 值\_调试器\_不\_存在。

 

 





