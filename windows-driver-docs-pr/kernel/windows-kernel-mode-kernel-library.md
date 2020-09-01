---
title: Windows 内核模式内核库
description: Windows 内核模式内核库
ms.assetid: e62264ee-5d52-4ae1-bd54-51e93c34762f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: deff3f336e045e0b8bd00fe5c33a947f96b36ba2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185375"
---
# <a name="windows-kernel-mode-kernel-library"></a>Windows 内核模式内核库

操作系统的 *内核* 将实现操作系统中的所有其他内容所依赖的核心功能。 Microsoft Windows 内核提供基本的低级操作，如计划线程或路由硬件中断。 它是操作系统的核心，其执行的所有任务都必须快速而简单。

向内核库提供直接接口的例程通常以 "**Ke**" 为前缀，例如， **KeGetCurrentThread**。 有关内核库例程的列表，请参阅 [内核库支持例程](/windows-hardware/drivers/ddi/_kernel/#core-kernel-library-support-routines)。

>[!NOTE]
>术语 *微内核* 不适用于 Windows 操作系统中使用的当前内核。