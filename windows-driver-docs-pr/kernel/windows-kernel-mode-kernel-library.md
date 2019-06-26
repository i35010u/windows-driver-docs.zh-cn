---
title: Windows 内核模式内核库
description: Windows 内核模式内核库
ms.assetid: e62264ee-5d52-4ae1-bd54-51e93c34762f
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4483335a8fc50525563d386a5b4324f43c6a0f5d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357981"
---
# <a name="windows-kernel-mode-kernel-library"></a>Windows 内核模式内核库


*内核*操作系统实现所有其他操作系统中依赖于的核心功能。 Microsoft Windows 内核提供了基本的低级操作，如计划线程或路由硬件中断。 它是操作系统的核心，它将执行的所有任务都必须都是快速而简单。

为提供内核库的直接接口的例程通常带有前缀"**Ke**"，例如**KeGetCurrentThread**。 有关内核库例程的列表，请参阅[内核库支持例程](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff542078(v=vs.85))。

**请注意**  术语*微内核*不适用于当前 Windows 操作系统中使用的内核。

 

 

 




