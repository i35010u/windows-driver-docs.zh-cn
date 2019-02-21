---
title: 调试 Bug 检查 0xC4 DRIVER_VERIFIER_DETECTED_VIOLATION
description: 如果驱动程序验证程序检测到冲突，它将生成的 bug 检查停止计算机。
ms.assetid: 4B957C57-9095-4C81-9EBC-C92C620C5824
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 872aa470c378f420910b21609589c9cf8eeed6cf
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524828"
---
# <a name="debugging-bug-check-0xc4-driververifierdetectedviolation"></a>调试 Bug 检查 0xC4:驱动程序\_VERIFIER\_检测到\_冲突


如果[Driver Verifier](driver-verifier.md)检测到冲突，它将生成的 bug 检查停止计算机。 这是为了向您提供可能的大多数信息用于调试问题。 一个更频繁的 bug 检查驱动程序验证程序生成是[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187)。 本部分介绍调试这些冲突的一些示例策略。

当[Driver Verifier](driver-verifier.md)问题[ **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187)，它使用的参数 1 值 （或子代码） 指定了冲突的具体原因。 **Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**检测到超过 200 个冲突。

## <a name="span-idinthissectionspanin-this-section"></a><span id="in_this_section"></span>在本部分中


-   [调试内存泄漏的驱动程序\_VERIFIER\_检测到\_冲突 (C4):0x62](debugging-memory-leaks---driver-verifier-detected-violation--c4---0x62.md)
-   [调试死锁的驱动程序\_VERIFIER\_检测到\_冲突 (C4):0x1001](debugging-deadlocks---driver-verifier-detected-violation--c4---0x1001.md)
-   [调试 DDI 符合性错误的驱动程序\_VERIFIER\_检测到\_冲突 (C4):0x20002 - 0x20022](debugging-ddi-compliance-bugs----driver-verifier-detected-violation--c4---0x000200--.md)
-   [调试 NDIS/WiFi 超时错误的驱动程序\_VERIFIER\_检测到\_冲突 (C4)](debugging-ndis-wifi-timeouts---driver-verifier-detected-violation--c4---0x92003--etc-.md)

## <a name="span-idprerequisitesspanspan-idprerequisitesspanspan-idprerequisitesspanprerequisites"></a><span id="Prerequisites"></span><span id="prerequisites"></span><span id="PREREQUISITES"></span>系统必备组件


-   运行[Driver Verifier](driver-verifier.md)保留用于测试的计算机上。
-   启用内核调试，在测试计算机上。

有关详细信息请参阅[Windows 调试](https://msdn.microsoft.com/library/windows/hardware/ff551063)并[处理 Bug 检查时驱动程序验证程序已启用](https://msdn.microsoft.com/library/windows/hardware/hh450984)。

 

 





