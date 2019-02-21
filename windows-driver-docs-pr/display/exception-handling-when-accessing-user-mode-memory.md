---
title: 访问用户模式内存时的异常处理
description: 访问用户模式内存时的异常处理
ms.assetid: 44ed69a0-da0e-4335-9128-a78a83ea80dd
keywords:
- 用户模式内存 WDK Windows 2000 显示
- 用户模式内存 WDK Windows 2000 显示异常处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a55b57c829e91642c3abcdb3b93ff5369d2a935
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524359"
---
# <a name="exception-handling-when-accessing-user-mode-memory"></a>访问用户模式内存时的异常处理


## <span id="ddk_exception_handling_when_accessing_user_mode_memory_gg"></span><span id="DDK_EXCEPTION_HANDLING_WHEN_ACCESSING_USER_MODE_MEMORY_GG"></span>


显示或微型端口驱动程序必须使用异常处理的访问的数据结构在用户模式下分配代码周围。 然后再将它们传递给驱动程序，Microsoft Direct3D 运行时保护此类数据结构的所有权。 安全所属权的用户模式内存中，运行时调用[ **MmSecureVirtualMemory** ](https://msdn.microsoft.com/library/windows/hardware/ff556374)函数。 当运行时保护的用户模式内存所有权时，它会阻止其他任何线程修改对内存的访问类型。 例如，如果运行时保护用户模式线程已分配与读取和写入访问的数据结构的所有权，其他线程不能将数据结构的访问类型限制为只读的。 此外，保护的用户模式内存所有权不保证内存保持有效。

因此，访问此类内存的代码周围实现异常处理，除非操作系统崩溃如果驱动程序将尝试访问无效的用户模式下的内存。 对于无效的内核内存访问，唯一可用的选项的操作系统是崩溃。 但是，对于无效的用户内存访问，该驱动程序可以终止失效内存的应用程序并处于稳定状态保留操作系统和驱动程序的设备。

该驱动程序必须实现异常处理而不是依赖于运行时来处理异常。 如果在运行时处理异常和驱动程序访问无效的用户模式内存，堆栈将返回到在运行时，该驱动程序或设备处于未知状态的异常处理代码。 该驱动程序必须实现异常处理，以便它可以执行以下操作，如果出现异常：

-   还原其状态以及其设备的状态。

-   释放它获取任何自旋锁。

在以下情况下，运行时保护将内存传递给驱动程序之前在用户模式下分配的内存的所有权。

-   该驱动程序处理指定的指向用户模式内存的指针的顶点数据。 驱动程序收到此内存指针在调用其[ **D3dDrawPrimitives2** ](https://msdn.microsoft.com/library/windows/hardware/ff544704)函数。 在此*D3dDrawPrimitives2*调用，D3DHALDP2\_USERMEMVERTICES 标记**dwFlags**隶属[ **D3DHAL\_DRAWPRIMITIVES2DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff545957)结构设置。

-   该驱动程序更新到的呈现状态数组**lpdwRStates** D3DHAL 成员\_DRAWPRIMITIVES2DATA 点。 驱动程序将更新此数组在调用其*D3dDrawPrimitives2*函数。

-   驱动程序将更新其状态**lpdwStates**的成员[ **DD\_GETDRIVERSTATEDATA** ](https://msdn.microsoft.com/library/windows/hardware/ff551551)结构调用其[ **D3dGetDriverState** ](https://msdn.microsoft.com/library/windows/hardware/ff544708)函数。

-   驱动程序位块传输或访问已分配的用户内存系统纹理。

显示驱动程序可以使用**试用 / 除外**机制来实现异常处理。 有关详细信息**试用 / 除外**，请参阅 Microsoft Visual c + + 文档。

下面的代码示例演示如何使用该驱动程序**试用 / 除外**机制因访问无效的内存而出错时引发异常。

```cpp
__try
{
    // Access user-mode memory.
}
__except(EXCEPTION_EXECUTE_HANDLER)
{
    // Recover and leave driver and hardware in a stable state.
}
```

**请注意**  除了访问，并将用户模式值复制到本地变量，驱动程序不应执行任何其他操作内的 **\_\_尝试**块。 其他操作可能导致其自己要发生的异常。 操作系统以不同方式处理这些异常。

 

 

 





