---
title: C28648
description: 警告 C28648 PulseEvent 是不可靠的函数。
ms.assetid: 6132e35c-f1ae-44cc-9a6c-b61d6e7f8c57
ms.date: 04/20/2017
ms.localizationpriority: medium
f1_keywords:
- C28648
ms.openlocfilehash: 3d171485cf2515030799d95b466c4f73d2831be5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564405"
---
# <a name="c28648"></a>C28648


警告 C28648:PulseEvent 是不可靠的函数

等待同步对象的线程可以暂时从等待状态删除由内核模式 APC，并后 APC 已完成，然后返回到等待状态。 如果在调用**PulseEvent**发生在该线程从等待状态已删除的时间段内，线程不会释放，并将"挂起"永远。 这是因为**PulseEvent**释放的就是目前正在等待的线程。

若要修复的使用方式的一些**PulseEvent**:

-   如果仅需要释放一个线程等待事件和事件是手动重置事件，则将其更改为自动重置事件，并调用**SetEvent**而不是**PulseEvent**。

-   如果仅需要释放一个线程等待事件和事件是一个自动重置事件，调用**SetEvent**而不是**PulseEvent**。

-   如果需要释放所有线程等待事件和事件是手动重置事件，重新设计代码以使用一种不同的同步对象 （如信号量）。

-   如果需要释放所有线程等待事件和事件是一个自动重置事件，调用**SetEvent**而不是**PulseEvent** (对原始调用**PulseEvent**已释放只有一个线程仍要）。

 

 





