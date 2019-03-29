---
title: 已检验版本和驱动程序验证程序
description: 已检验版本和驱动程序验证程序
ms.assetid: 311a9588-5094-432c-b696-339ff3ff8c35
keywords:
- 检查内部版本号 WDK，驱动程序验证程序
- 检查驱动程序验证程序 WDK 构建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab66cf60ab0dc6a0565b1a68b665c51b41a1fcb2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568773"
---
# <a name="the-checked-build-and-driver-verifier"></a>已检验版本和驱动程序验证程序


## <span id="ddk_the_checked_build_and_driver_verifier_tools"></span><span id="DDK_THE_CHECKED_BUILD_AND_DRIVER_VERIFIER_TOOLS"></span>


尽管已检验的版本和[Driver Verifier](driver-verifier.md)提供一些检查，重叠，最好是将它们视为提供补充级别的检查。 在测试与已检验版本驱动程序不能代替使用驱动程序验证程序进行测试。 同样，使用驱动程序验证程序进行测试不提供精确相同级别的测试覆盖率与使用已检验的版本。

驱动程序验证程序上运行时已检验版本，它通常显示的其他信息在调试器中检测到问题时。 此外，当附加有调试器，在许多情况下驱动程序验证程序在运行前停止系统的 bug 检查断点。 此断点，您可以检查系统的状态和调试驱动程序、 驱动程序验证工具调用系统崩溃前的机会。

 

 





