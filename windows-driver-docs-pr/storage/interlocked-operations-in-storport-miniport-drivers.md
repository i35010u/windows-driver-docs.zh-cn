---
title: Storport 微型端口驱动程序中的互锁的操作
description: 适用于 Windows 应用程序的许多互锁函数适用于 Storport 微型端口驱动程序。
ms.assetid: F3868AF4-545F-4B8E-8655-5AAD888C4B40
ms.date: 06/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 90bba217d54462d0f6d0acc4ec21e70c7f2d79aa
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188937"
---
# <a name="interlocked-operations-in-storport-miniport-drivers"></a>Storport 微型端口驱动程序中的互锁的操作

应用程序必须同步对多个线程共享的变量的访问，使用平台软件开发工具包 (SDK) 互锁函数来执行此操作。 适用于 Windows 应用程序的许多互锁函数适用于 Storport 微型端口驱动程序。 其中的大多数函数作为 [编译器内部函数](/cpp/intrinsics/compiler-intrinsics?view=vs-2019) 实现，适用于同步对受保护的值所做的更改。
为逻辑、赋值、比较和算术运算定义函数。

有关联锁操作的详细信息，请参阅 [联锁变量访问](/windows/desktop/Sync/interlocked-variable-access)。

**注意** **联锁 * Xxx*** 函数在基于 *微型端口 .h* 中声明，对于32位 (x86) 驱动程序，则在 *storport. h*中声明。