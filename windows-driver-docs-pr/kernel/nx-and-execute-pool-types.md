---
title: NX 和执行池类型
description: 若要指示是否从非分页缓冲池分配的内存应为无执行 (NX)，可以使用从 Windows 8 开始的两个新池类型。
ms.assetid: 954AC53F-270D-4149-AE5D-6BEA7EFAA761
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 80005e402a39364e216abc304da1c6d90a8ec0ce
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577430"
---
# <a name="nx-and-execute-pool-types"></a>NX 和执行池类型


若要指示是否从非分页缓冲池分配的内存应为无执行 (NX)，可以使用从 Windows 8 开始的两个新池类型。 这些池类型指定由以下[**池\_类型**](https://msdn.microsoft.com/library/windows/hardware/ff559707)枚举值：

<a href="" id="nonpagedpoolnx"></a>**NonPagedPoolNx**  
NX 非分页缓冲的池。 不能从这个池分配的内存中执行的说明。

<a href="" id="nonpagedpoolexecute"></a>**NonPagedPoolExecute**  
可执行文件的非分页缓冲的池。 从这个池分配的内存中启用指令执行。

大多数驱动程序仅使用已分配的内存存储数据，并不执行此内存中的说明。 如果您的驱动程序在 Windows 8 和更高版本的 Windows 上运行生成时，将分配**NonPagedPoolNx** NX 内存只要有可能的非分页缓冲的池。 仅从非分页内存执行指令所需要的驱动程序应分配**NonPagedPoolExecute**从可执行文件的非分页缓冲池的内存。

当你使用时为 Windows 7 和早期版本的 Windows，生成的现有驱动程序**非分页池**池类型驱动程序从可执行文件的池中分配内存。 **非分页池**常量的名称具有相同的值**NonPagedPoolExecute**从 Windows 8 开始定义的常量名称。 因此，这些常量引用相同的池类型。

如果编写的 Windows 7 或 Windows 的早期版本的驱动程序专为 Windows 8 或更高版本的 Windows 的实例**非分页池**池类型应替换为通过以下任一方式**NonPagedPoolNx**或**NonPagedPoolExecute**。 驱动程序开发人员可以显式执行此替换，或可以隐式使用一种选择的机制，可用于帮助开发人员将在移植到 Windows 8 其驱动程序执行替换。 有关详细信息，请参阅[NX 池选择的机制](nx-pool-opt-in-mechanisms.md)。

 

 




