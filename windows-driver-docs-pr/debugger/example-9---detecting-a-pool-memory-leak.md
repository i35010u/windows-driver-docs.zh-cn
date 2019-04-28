---
title: 示例 9 检测池内存泄漏
description: 示例 9 检测池内存泄漏
ms.assetid: 3f634593-a024-46d1-9f3d-9d39b28bab03
keywords:
- PoolMon、 PoolMon 和 GFlags
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: f4a193fbd6a2d17964f3d7478c92eb789b116e45
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63344155"
---
# <a name="example-9-detecting-a-pool-memory-leak"></a>示例 9：检测池内存泄漏


## <span id="ddk_example_9___detecting_a_pool_memory_leak_dtools"></span><span id="DDK_EXAMPLE_9___DETECTING_A_POOL_MEMORY_LEAK_DTOOLS"></span>


下面的示例使用 GFlags 设置系统级[启用池标记](enable-pool-tagging.md)注册表中的标志。 然后，它使用 PoolMon (poolmon.exe) 的工具在 Windows 驱动程序工具包中，若要显示的内存池的大小。

PoolMon 监视中的分页和非分页内存池字节数，并按池标记进行排序。 通过定期运行 PoolMon，可以标识的不断地随时间扩展应用程序池。 此模式通常指示内存泄漏。

**请注意**  标记池永久中启用了 Windows Server 2003 和更高版本的 Windows。 在这些系统上**启用池标记**上的复选框**全局标志**对话框灰显，并且命令来启用或禁用池标记失败。
如果未启用池标记，PoolMon 会失败并显示以下消息："查询 pooltags 失败 c0000002。"

 

**若要检测池的内存泄漏**

1.  若要启用池标记为早于 Windows Server 2003 的 Windows 版本中的所有进程，设置系统级[启用池标记](enable-pool-tagging.md)注册表中的标志。 下面的命令行使用标志缩写方法，但您可以通过其十六进制值标识标志或使用**全局标志**对话框：
    ```console
    gflags /r +ptg 
    ```

2.  重新启动计算机以使注册表更改生效。

3.  定期运行 PoolMon 中使用以下命令。 在此命令中， **b </b**参数进行排序以降序大小的池。

    ```console
    poolmon /b 
    ```

    在响应中，从按降序大小包括的数量的内存池 PoolMon 显示分配分配操作和 free 操作和 （以字节数列中） 池中剩余的内存量。

    ```console
    Memory: 16224K Avail: 4564K PageFlts: 31 InRam Krnl: 684K P: 680K
     Commit: 24140K Limit: 24952K Peak: 24932K  Pool N: 744K P: 2180K

     Tag  Type    Allocs          Frees         Diff   Bytes      Per Alloc
    -----------------------------------------------------------------------

     CM   Paged    1283 (   0)    1002 (   0)    281 1377312 (     0) 4901
    Strg  Paged   10385 (  10)    6658 (   4)   3727  317952 (   512)   85
     Fat  Paged    6662 (   8)    4971 (   6)   1691  174560 (   128)  103
    MmSt  Paged     614 (   0)     441 (   0)    173   83456 (     0)  482
    ```

    如果中的值**字节**列分配持续扩展没有明显原因，在该池中可能内存泄漏。

4.  清除**启用池标记**标志。

    下面的命令行使用标志缩写方法，但您可以通过其十六进制值标识标志或使用**全局标志**对话框：

    ```console
    gflags /r -ptg 
    ```

5.  重新启动 Windows 以使注册表更改生效。

**请注意**  使用追加符号 (**&gt;&gt;**) PoolMon 输出重定向到日志文件。 更高版本，可以检查池大小趋势的日志文件。 例如：

 

```console
poolmon.exe /b >> poolmon.log 
```

 

 





