---
title: Windows 内核模式内核库
description: Windows 内核模式内核库
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b5ed565afa04d1245f815215aef195bbe4c120d4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837941"
---
# <a name="windows-kernel-mode-kernel-library"></a>Windows 内核模式内核库

操作系统的 *内核* 将实现操作系统中的所有其他内容所依赖的核心功能。 Microsoft Windows 内核提供基本的低级操作，如计划线程或路由硬件中断。 它是操作系统的核心，其执行的所有任务都必须快速而简单。

向内核库提供直接接口的例程通常以 "**Ke**" 为前缀，例如， **KeGetCurrentThread**。 有关内核库例程的列表，请参阅 [内核库支持例程](/windows-hardware/drivers/ddi/_kernel/#core-kernel-library-support-routines)。

>[!NOTE]
>术语 *微内核* 不适用于 Windows 操作系统中使用的当前内核。
