---
title: 确定是否已附加调试器
description: 确定是否已附加调试器
ms.assetid: b40482c4-7186-4632-b1d9-3c91a415b7c8
keywords:
- 调试代码 WDK，附加调试器
- 附加调试器 WDK
- 状态信息 WDK 调试
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dc3dc5c034c6e26646c9e929cadaa9d1f934186d
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840281"
---
# <a name="determining-if-a-debugger-is-attached"></a>确定是否已附加调试器


## <span id="ddk_determining_if_a_debugger_is_attached_tools"></span><span id="DDK_DETERMINING_IF_A_DEBUGGER_IS_ATTACHED_TOOLS"></span>


如果当前附加了内核调试器，你可能希望对驱动程序执行某些操作。

若要确定内核调试的状态，以下变量和例程非常有用：

-   （Microsoft Windows XP 及更高版本）[**KD\_调试程序\_启用**](https://docs.microsoft.com/previous-versions/ff548118(v=vs.85))的全局内核变量指示是否启用内核调试。

-   （Windows XP 及更高版本）[**KD\_调试器\_不\_存在**](https://docs.microsoft.com/previous-versions/ff548125(v=vs.85))的全局内核变量指示当前是否附加了内核调试器。

-   （Microsoft Windows Server 2003 及更高版本）[**KdRefreshDebuggerNotPresent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-kdrefreshdebuggernotpresent)例程刷新 KD\_调试程序\_不\_存在的值。

 

 





