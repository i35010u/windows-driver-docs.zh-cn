---
title: 访问用户模式内存时处理异常
description: 访问用户模式内存时处理异常
ms.assetid: 44ed69a0-da0e-4335-9128-a78a83ea80dd
keywords:
- 用户模式内存 WDK Windows 2000 显示
- 用户模式内存 WDK Windows 2000 显示，异常处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f94333dfa7a5264dd55cf3a9af2b59c5760472e4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838945"
---
# <a name="exception-handling-when-accessing-user-mode-memory"></a>访问用户模式内存时处理异常


## <span id="ddk_exception_handling_when_accessing_user_mode_memory_gg"></span><span id="DDK_EXCEPTION_HANDLING_WHEN_ACCESSING_USER_MODE_MEMORY_GG"></span>


显示或视频微型端口驱动程序必须围绕访问在用户模式中分配的数据结构的代码使用异常处理。 在将此类数据结构传递给驱动程序之前，Microsoft Direct3D 运行时将保护其所有权。 为了确保用户模式内存的所有权，运行时调用[**MmSecureVirtualMemory**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddk/nf-ntddk-mmsecurevirtualmemory)函数。 当运行时保护用户模式内存的所有权时，它会阻止任何其他线程修改对内存的访问类型。 例如，如果运行时使用读取和写入访问权限来保护数据结构的所有权，则其他线程无法将数据结构的访问类型限制为只读。 此外，保护用户模式内存的所有权不能保证内存保持有效。

因此，除非在访问此类内存的代码周围实现了异常处理，否则，如果驱动程序尝试访问无效的用户模式内存，操作系统就会崩溃。 对于内核内存访问无效，操作系统唯一可用的选项是 "崩溃"。 但对于无效的用户内存访问，驱动程序可以终止使内存失效的应用程序，并使操作系统和驱动程序的设备处于稳定状态。

驱动程序必须实现异常处理，而不是依赖于运行时来处理异常。 如果运行时处理异常并且驱动程序访问了无效的用户模式内存，堆栈将返回到运行时中的异常处理代码，使驱动程序或设备处于未知状态。 驱动程序必须实现异常处理，以便在发生异常的情况下，它可以执行以下操作：

-   还原其状态和其设备的状态。

-   释放它获取的任何自旋锁。

在以下情况下，运行时在将内存传递给驱动程序之前，将在用户模式下保护分配的内存的所有权。

-   驱动程序将指针指定的顶点数据处理到用户模式内存。 驱动程序会在对其[**D3dDrawPrimitives2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数的调用中接收此内存指针。 在此*D3dDrawPrimitives2*调用中，将设置[**D3DHAL\_DRAWPRIMITIVES2DATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_drawprimitives2data)结构的**DWFLAGS**成员的 D3DHALDP2\_USERMEMVERTICES 标志。

-   驱动程序将 D3DHAL 的**lpdwRStates**成员\_DRAWPRIMITIVES2DATA 点的呈现状态数组更新。 驱动程序在调用其*D3dDrawPrimitives2*函数时更新此数组。

-   驱动程序在调用其[**D3dGetDriverState**](https://docs.microsoft.com/windows/desktop/api/ddrawint/nc-ddrawint-pdd_getdriverstate)函数的过程中，在[**DD\_GETDRIVERSTATEDATA**](https://docs.microsoft.com/windows/desktop/api/ddrawint/ns-ddrawint-_dd_getdriverstatedata)结构的**lpdwStates**成员上更新其状态。

-   驱动程序位块传输或访问在用户内存中分配的系统纹理。

显示驱动程序可以使用**try/except**机制来实现异常处理。 有关**try/except**的详细信息，请参阅 Microsoft Visual C++文档。

下面的代码示例演示当因访问无效内存而导致错误时，驱动程序如何使用**try/except**机制来引发异常。

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

**请注意**，   除了访问用户模式值并将其复制到本地变量，驱动程序不应在 **\_\_try**块中执行任何其他操作。 其他操作可能会导致其例外。 操作系统处理这些异常的方式不同。

 

 

 





