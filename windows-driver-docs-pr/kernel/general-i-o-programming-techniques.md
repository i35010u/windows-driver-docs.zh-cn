---
title: 常规 I/O 编程技术
description: 常规 I/O 编程技术
ms.assetid: c310829f-e102-4a96-aa3e-39136b8a641b
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d0441ff7e12e6ada42b5d46d8836a22f929bf517
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56556065"
---
# <a name="general-io-programming-techniques"></a>常规 I/O 编程技术


I/O 编程中最重要的技术之一是指应避免： 强制等待你的设备的操作系统。 几乎每个人都有必须查看 Microsoft Windows 的"冻结"的体验。 有时会冻结是因为崩溃，但其他情况下系统只需等待设备响应。

有两种基本编程技术来处理与正在等待设备：*同步*并*异步*。 同步编程等待设备，应当避免。 异步编程使用其他技术 （例如等待中断请求）。 有关同步和异步编程的详细信息，请参阅以下主题：

[同步 I/O 编程](synchronous-i-o-programming.md)

[异步 I/O 编程](asynchronous-i-o-programming.md)

Microsoft Vista 有新的策略来应对同步编程的问题。 有关此新策略的详细信息，请参阅[限制等待 Windows Vista 中](restricting-waits-in-vista.md)有关详细信息。

在编程早期的设备驱动程序，驱动程序将需要重复请求某个驱动程序的信息，直到提供答案。 此技术称为轮询，几乎总是不应使用。 处理轮询该问题的最佳方式是使用硬件中断。 有关硬件中断的详细信息，请参阅[服务中断](servicing-interrupts.md)。 轮询和为什么您不应使用它的详细信息，请参阅[避免设备轮询](avoid-polling-devices.md)。

 

 




