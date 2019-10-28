---
title: NX 和执行池类型
description: 若要指示从非分页池分配的内存是否应为非执行（NX），可以使用从 Windows 8 开始的两个新池类型。
ms.assetid: 954AC53F-270D-4149-AE5D-6BEA7EFAA761
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 9d79d7e676f2c595d34a11a004091f181a7d9f7c
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838536"
---
# <a name="nx-and-execute-pool-types"></a>NX 和执行池类型


若要指示从非分页池分配的内存是否应为非执行（NX），可以使用从 Windows 8 开始的两个新池类型。 这些池类型由以下[**池指定\_类型**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_pool_type)枚举值：

<a href="" id="nonpagedpoolnx"></a>**NonPagedPoolNx**  
NX 非分页池。 无法在从此池分配的内存中执行指令。

<a href="" id="nonpagedpoolexecute"></a>**NonPagedPoolExecute**  
可执行的非分页池。 在从此池分配的内存中启用了指令执行。

大多数驱动程序只使用分配的内存来存储数据，而不执行此内存中的指令。 如果生成要在 Windows 8 和更高版本的 Windows 上运行的驱动程序，请尽可能从 NX 非分页池分配**NonPagedPoolNx**内存。 只有需要从非分页内存执行指令的驱动程序才能从可执行的非分页池分配**NonPagedPoolExecute**内存。

对于为 Windows 7 和更早版本的 Windows 构建的现有驱动程序，当你使用**非分页池**池类型时，你的驱动程序将从可执行池中分配内存。 **非分页池**常量名称与从 Windows 8 开始定义的**NonPagedPoolExecute**常量名称具有相同的值。 因此，这些常量引用相同的池类型。

如果为 windows 7 或更早版本的 windows 生成的驱动程序是为 Windows 8 或更高版本的 windows 构建的，则应将**非分页池**池类型的实例替换为**NonPagedPoolNx**或**NonPagedPoolExecute**。 驱动程序开发人员可以显式执行此替换，也可以通过使用提供的一种选择加入机制来隐式执行替换，以帮助开发人员将其驱动程序移植到 Windows 8。 有关详细信息，请参阅[NX 池选择加入机制](nx-pool-opt-in-mechanisms.md)。

 

 




