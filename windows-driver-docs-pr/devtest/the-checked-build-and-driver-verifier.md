---
title: 已检验版本和驱动程序验证程序
description: 已检验版本和驱动程序验证程序
keywords:
- 检查生成 WDK，驱动程序验证程序
- 驱动程序验证程序 WDK 检查生成
ms.date: 06/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: fc13d798302996a0fdadf2b53b4fa059b252c625
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817425"
---
# <a name="the-checked-build-and-driver-verifier"></a>已检验版本和驱动程序验证程序

尽管检查的生成和 [驱动程序验证程序](driver-verifier.md) 提供了一些重叠的检查，但最好将它们视为提供更互补的检查级别。 使用所选版本测试驱动程序不能代替使用驱动程序验证程序进行测试。 同样，使用 "驱动程序验证程序" 进行测试并不提供与使用所选版本相同的测试覆盖率级别。

当驱动程序验证器在检查的生成上运行时，它通常会在检测到问题时显示在调试器中的其他信息。 此外，在附加调试器的情况下，在使用 bug 检查停止系统之前，驱动程序验证程序会运行一个断点。 在出现驱动程序验证程序调用系统崩溃之前，此断点使你有机会检查系统的状态并调试驱动程序。

> [!NOTE]
> 在 Windows 10 版本1803之前，已检查的生成在较早版本的 Windows 上可用。
> 使用驱动程序验证程序和 GFlags 等工具在更高版本的 Windows 中检查驱动程序代码。
