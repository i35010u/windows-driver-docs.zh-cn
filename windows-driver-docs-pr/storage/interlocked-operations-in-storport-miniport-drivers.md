---
title: Storport 微型端口驱动程序中的互锁的操作
description: 适用于 Windows 应用程序的许多互锁函数适用于 Storport 微型端口驱动程序。
ms.assetid: F3868AF4-545F-4B8E-8655-5AAD888C4B40
ms.date: 06/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6e9b3f2d61225419ddd8bd58c4892b0336db5188
ms.sourcegitcommit: 238308264c1ee2c74ec0c8c303258dc00c79b902
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2019
ms.locfileid: "70063908"
---
# <a name="interlocked-operations-in-storport-miniport-drivers"></a>Storport 微型端口驱动程序中的互锁的操作

应用程序必须同步对多个线程共享的变量的访问, 使用平台软件开发工具包 (SDK) 互锁函数执行此操作。 适用于 Windows 应用程序的许多互锁函数适用于 Storport 微型端口驱动程序。 其中的大多数函数作为[编译器内部函数](https://docs.microsoft.com/cpp/intrinsics/compiler-intrinsics?view=vs-2019)实现, 适用于同步对受保护的值所做的更改。
为逻辑、赋值、比较和算术运算定义函数。

有关联锁操作的详细信息, 请参阅[联锁变量访问](https://docs.microsoft.com/windows/desktop/Sync/interlocked-variable-access)。

**请注意**  ,**联锁 * Xxx*** 函数是在*微型端口 .h*中声明的, 对于32位 (x86) 驱动程序, 则在*storport. h*中声明。