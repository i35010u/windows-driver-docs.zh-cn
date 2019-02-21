---
title: Windows 内核模式内核库
description: Windows 内核模式内核库
ms.assetid: e62264ee-5d52-4ae1-bd54-51e93c34762f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 45bd22b0bd5b4ff743fcf9f73d4e38e7b8d37e23
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521755"
---
# <a name="windows-kernel-mode-kernel-library"></a>Windows 内核模式内核库


*内核*操作系统实现所有其他操作系统中依赖于的核心功能。 Microsoft Windows 内核提供了基本的低级操作，如计划线程或路由硬件中断。 它是操作系统的核心，它将执行的所有任务都必须都是快速而简单。

为提供内核库的直接接口的例程通常带有前缀"**Ke**"，例如**KeGetCurrentThread**。 有关内核库例程的列表，请参阅[内核库支持例程](https://msdn.microsoft.com/library/windows/hardware/ff542078)。

**请注意**  术语*微内核*不适用于当前 Windows 操作系统中使用的内核。

 

 

 




