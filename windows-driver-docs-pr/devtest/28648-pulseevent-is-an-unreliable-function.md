---
title: C28648
description: 警告 C28648 PulseEvent 是一种不可靠的函数。
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28648
ms.openlocfilehash: b46354f750d6ee0f3039cb57ff505f48d26bb3c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840195"
---
# <a name="c28648"></a>C28648


警告 C28648： PulseEvent 是不可靠的函数

等待同步对象的线程可以通过内核模式 APC 暂时从等待状态中删除，然后在 APC 完成后返回到等待状态。 如果在线程从等待状态中移除时，对 **PulseEvent** 的调用发生，则不会释放该线程，并将永远 "挂起"。 这是因为， **PulseEvent** 仅释放在调用它时等待的线程。

修复 **PulseEvent** 使用的一些方法：

-   如果只需要释放一个等待事件的线程，并且事件为手动重置事件，请将其更改为自动重置事件，并调用 **SetEvent** 而不是 **PulseEvent**。

-   如果只需要释放一个等待事件的线程，并且事件为自动重置事件，请调用 **SetEvent** 而不是 **PulseEvent**。

-   如果需要释放所有等待事件的线程，并且事件是手动重置事件，请重新设计代码，以使用不同类型的同步对象 (如信号量) 。

-   如果每个等待事件的线程都需要释放，并且事件是自动重置事件，请调用 **SetEvent** 而不是 **PulseEvent** (你对 **PulseEvent** 的原始调用仅) 一个线程。

 

 





