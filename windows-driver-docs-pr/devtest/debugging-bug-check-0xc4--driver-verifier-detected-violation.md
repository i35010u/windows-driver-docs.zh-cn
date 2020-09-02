---
title: 调试 Bug 检查 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION
description: 如果驱动程序验证程序检测到冲突，则会生成 bug 检查来停止计算机。
ms.assetid: 4B957C57-9095-4C81-9EBC-C92C620C5824
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 45043442951ef1f1278a17e90acdccfb5ba183a9
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89382371"
---
# <a name="debugging-bug-check-0xc4-driver_verifier_detected_violation"></a>调试 Bug 检查0xC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突


如果 [驱动程序验证程序](driver-verifier.md) 检测到冲突，则会生成 bug 检查来停止计算机。 这是为了提供用于调试问题的最大信息。 Bug 检查中的一个更常见的 bug 检查会生成 [**Bug 检查0xC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md)。 本部分介绍用于调试这些冲突的一些示例策略。

当 [驱动程序验证](driver-verifier.md) 器发出 [**Bug 检查0XC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md)时，它将使用参数1值 (或子代码) 来指定冲突的特定原因。 **Bug 检查0xC4：驱动程序 \_\_检测到 \_ 的验证器冲突**检测超过200违规。

## <a name="span-idin_this_sectionspanin-this-section"></a><span id="in_this_section"></span>本部分中的内容


-   [调试内存泄漏-驱动程序 \_ 验证器 \_ 检测到 \_ 违反 (C4) ：0x62](debugging-memory-leaks---driver-verifier-detected-violation--c4---0x62.md)
-   [调试死锁-驱动程序 \_ 验证器 \_ 检测到 \_ 违反 (C4) ：0x1001](debugging-deadlocks---driver-verifier-detected-violation--c4---0x1001.md)
-   [调试 DDI 相容性错误-驱动程序 \_ 验证器 \_ 检测到 \_ 违反 (C4) ： 0x20002-0x20022](debugging-ddi-compliance-bugs----driver-verifier-detected-violation--c4---0x000200--.md)
-   [调试 NDIS/WiFi 超时错误-驱动程序 \_ 验证器 \_ 检测到 \_ 违反 (C4) ](debugging-ndis-wifi-timeouts---driver-verifier-detected-violation--c4---0x92003--etc-.md)

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>先决条件


-   在保留用于测试的计算机上运行 [驱动程序验证程序](driver-verifier.md) 。
-   在测试计算机上启用内核调试。

有关详细信息，请参阅 [Windows 调试](../debugger/index.md) 和 [处理启用驱动程序验证程序时的 Bug 检查](../debugger/handling-a-bug-check-when-driver-verifier-is-enabled.md)。

 

