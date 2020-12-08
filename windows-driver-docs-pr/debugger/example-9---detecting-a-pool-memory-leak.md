---
title: 示例9检测池内存泄漏
description: 示例9检测池内存泄漏
keywords:
- PoolMon、PoolMon 和 GFlags
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: bffe34053c3fde6c6debbc40195e6b1a367ba958
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838223"
---
# <a name="example-9-detecting-a-pool-memory-leak"></a>示例9：检测池内存泄漏


## <span id="ddk_example_9___detecting_a_pool_memory_leak_dtools"></span><span id="DDK_EXAMPLE_9___DETECTING_A_POOL_MEMORY_LEAK_DTOOLS"></span>


下面的示例使用 GFlags 在注册表中设置系统范围的 [启用池标记](enable-pool-tagging.md) 标记。 然后，它使用 PoolMon ( # A0) （Windows 驱动程序工具包中的工具）来显示内存池的大小。

PoolMon 监视分页和非分页内存池的字节数，并按池标记对它们进行排序。 通过定期运行 PoolMon，你可以识别随着时间推移不断扩展的池。 此模式通常指示内存泄漏。

**注意**   池标记在 Windows Server 2003 和更高版本的 Windows 中被永久启用。 在这些系统中，"**全局标志**" 对话框中的 "**启用池标记**" 复选框将灰显，启用或禁用池标记的命令将失败。
如果未启用池标记，则 PoolMon 会失败，并显示以下消息： "Query pooltags Failed c0000002."

 

**检测池内存泄漏**

1.  若要为早于 Windows Server 2003 的 Windows 版本中的所有进程启用池标记，请在注册表中设置系统范围的 [启用池标记](enable-pool-tagging.md) 标记。 以下命令行使用标志缩写方法，但你可以通过其十六进制值标识该标志或使用 " **全局标志** " 对话框：
    ```console
    gflags /r +ptg 
    ```

2.  重新启动计算机，使注册表更改生效。

3.  使用以下命令定期运行 PoolMon。 在此命令中， **/b** 参数按降序调整池的大小。

    ```console
    poolmon /b 
    ```

    在响应中，PoolMon 按大小的降序显示内存池中的分配，包括分配操作和自由操作的数目，以及池中 (的字节列中的剩余内存量) 。

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

    如果分配的 **字节** 列中的值连续扩展，则可能是该池中存在内存泄漏。

4.  清除 " **启用池标记** " 标志。

    以下命令行使用标志缩写方法，但你可以通过其十六进制值标识该标志或使用 " **全局标志** " 对话框：

    ```console
    gflags /r -ptg 
    ```

5.  重新启动 Windows，使注册表更改生效。

**注意**   使用追加符号 (**&gt;&gt;**) 将 PoolMon 输出重定向到日志文件。 稍后，你可以检查日志文件中的池大小趋势。 例如：

 

```console
poolmon.exe /b >> poolmon.log 
```

 

 





