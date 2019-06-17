---
title: Storport 微型端口驱动程序中的互锁的操作
description: 许多可用于 Windows 应用程序的互锁函数都适合于 Storport 微型端口驱动程序中使用。
ms.assetid: F3868AF4-545F-4B8E-8655-5AAD888C4B40
ms.date: 06/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: e9b52cbbace16d260ff34fb72546d56fd0f54563
ms.sourcegitcommit: 91b989fc3256267fab89c36b1fa54ff039dcc687
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "67148524"
---
# <a name="interlocked-operations-in-storport-miniport-drivers"></a>Storport 微型端口驱动程序中的互锁的操作

应用程序必须同步对共享的多个线程，使用平台软件开发工具包 (SDK) 互锁函数来执行此操作的变量的访问。 许多可用于 Windows 应用程序的互锁函数都适合于 Storport 微型端口驱动程序中使用。 其中的大多数功能作为实现[编译器内部函数](https://docs.microsoft.com/cpp/intrinsics/compiler-intrinsics?view=vs-2019)和适用于将更改同步到受保护的值。
函数定义的逻辑，赋值、 比较和算术运算。

互锁操作有关的详细信息，请参阅[联锁变量访问](https://docs.microsoft.com/en-us/windows/desktop/Sync/interlocked-variable-access)。

**请注意**   **Interlocked * Xxx*** 的函数中声明*miniport.h*或 32 位 (x86) 驱动程序，请在*storport.h*。