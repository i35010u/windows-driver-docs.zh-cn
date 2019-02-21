---
title: 了解的 Static Driver Verifier
description: 了解的 Static Driver Verifier
ms.assetid: 519e3314-2fea-4acd-8c0d-954a57e257ba
keywords:
- WDK，关于 Static Driver Verifier 的 static Driver Verifier
- StaticDV WDK，关于 Static Driver Verifier
- SDV WDK，关于 Static Driver Verifier
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c95e67345779c9b5e003319e50cd8b2b4e79cec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547790"
---
# <a name="understanding-static-driver-verifier"></a>了解的 Static Driver Verifier


若要编写符合 Windows 驱动程序模型 (WDM) 或内核模式驱动程序框架 (KMDF)、 NDIS 或 Storport 的可靠驱动程序，必须具备专业知识并了解该驱动程序与 I/O 管理器交互的方式。 测试这些驱动程序是同样棘手。

开发可靠的驱动程序可能具有挑战性的原因如下：

-   驱动程序是异步的即使在单处理器计算机上。

-   驱动程序是高度可重入。

-   驱动程序使用许多奇怪的规则。

-   驱动程序模型是发展，随着时间的推移 age。

测试设备驱动程序限制由以下原因：

-   *观察*。 您不能观察到驱动程序和操作系统之间的交互中的错误。 驱动程序可以违反隐式使用规则，从而导致故障或不正确的行为，但很难检测到开发和测试驱动程序时出现错误的根本原因。

-   *控制*。 在正常情况下正常工作的驱动程序可以仅出现在发生异常情况，例如当它下面堆栈中的驱动程序失败时 IRP 的细微错误。 这种情况下难以进行，因此传统测试不会充分检测通过驱动程序代码的错误路径。

SDV 增强了的观察和测试驱动程序时遇到的控件。 通过定义适当使用 WDM、 KMDF、 NDIS 和 Storport 函数的规则和监视这些规则的驱动程序的符合性，SDV 可以提高您发现错误的能力。 例如，WDM 规则[LowerDriverReturn](https://msdn.microsoft.com/library/windows/hardware/ff548273)指定，在某些情况下，驱动程序的调度例程应始终返回堆栈中较低的驱动程序返回的值。

SDV 也会增加通过提供的控件：

-   驱动程序的环境中，（例如操作系统调用连续失败） 的几个最坏情况可能恶意模型。

-   功能强大的静态分析 (称为*模型检查*) 的系统地探讨了驱动程序中的所有可能的执行路径。

SDV 是设备驱动程序的基本单元测试工具。 将驱动程序放在恶意环境中并系统地测试代码路径通过驱动程序通过查找驱动程序模型使用规则的冲突。

 

 





