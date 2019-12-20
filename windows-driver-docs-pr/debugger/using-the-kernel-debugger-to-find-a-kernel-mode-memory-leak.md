---
title: 使用内核调试程序查找内核模式内存泄漏
description: 使用内核调试程序查找内核模式内存泄漏
ms.assetid: eeadd505-b887-498d-9369-877156526355
keywords:
- 内存泄漏，内核模式，内核调试器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0398237fbd88fb8afd1f68d98b743c95bb32035f
ms.sourcegitcommit: d30691c8276f7dddd3f8333e84744ddeea1e1020
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/19/2019
ms.locfileid: "75209627"
---
# <a name="using-the-kernel-debugger-to-find-a-kernel-mode-memory-leak"></a>使用内核调试程序查找内核模式内存泄漏


内核调试器确定内核模式内存泄漏的确切位置。

### <a name="span-idenable_pool_tagging__windows_2000_and_windows_xp_spanspan-idenable_pool_tagging__windows_2000_and_windows_xp_spanenable-pool-tagging"></a><span id="enable_pool_tagging__windows_2000_and_windows_xp_"></span><span id="ENABLE_POOL_TAGGING__WINDOWS_2000_AND_WINDOWS_XP_"></span>启用池标记 

必须首先使用[GFlags](gflags.md)来启用池标记。 GFlags 包含在 Windows 调试工具中。 启动 GFlags，选择 "**系统注册表**" 选项卡，选中 "**启用池标记**" 框，然后单击 "**应用**"。 您必须重新启动 Windows 才能使此设置生效。

在 Windows Server 2003 和更高版本的 Windows 上，始终启用池标记。

### <a name="span-iddetermining_the_pool_tag_of_the_leakspanspan-iddetermining_the_pool_tag_of_the_leakspandetermining-the-pool-tag-of-the-leak"></a><span id="determining_the_pool_tag_of_the_leak"></span><span id="DETERMINING_THE_POOL_TAG_OF_THE_LEAK"></span>确定泄漏的池标记

若要确定与该泄漏关联的池标记，通常使用 PoolMon 工具执行此步骤。 有关详细信息，请参阅[使用 PoolMon 查找内核模式的内存泄漏](using-poolmon-to-find-a-kernel-mode-memory-leak.md)。

此外，还可以使用内核调试器查找与大型池分配关联的标记。 为此，请执行此过程：

1.  使用[**. reload.sql （重新加载模块）**](-reload--reload-module-.md)命令重载所有模块。

2.  使用[**！ poolused**](-poolused.md)扩展。 包含标记 "4"，以通过分页内存使用对输出进行排序：
    ```dbgcmd
    kd> !poolused 4 
    Sorting by Paged Pool Consumed

    Pool Used:
                NonPaged            Paged     
    Tag    Allocs     Used    Allocs     Used 
    Abc         0        0     36405 33930272 
    Tron        0        0       552  7863232 
    IoN7        0        0     10939   998432 
    Gla5        1      128      2222   924352 
    Ggb         0        0        22   828384 
    ```

3.  确定哪个池标记与最大内存用量相关联。 在此示例中，使用标记 "Abc" 的驱动程序使用最大内存（几乎 34 MB）。 因此，内存泄漏最可能位于此驱动程序中。

### <a name="span-idfinding_the_leakspanspan-idfinding_the_leakspanfinding-the-leak"></a><span id="finding_the_leak"></span><span id="FINDING_THE_LEAK"></span>查找泄漏

确定与泄漏关联的池标记后，请按照此过程来查找泄漏本身：

1.  使用[**ed （输入值）**](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)命令修改 global 系统变量**PoolHitTag**的值。 当使用与值匹配的池标记时，此全局变量使调试器中断。

2.  将**PoolHitTag**设置为您怀疑是内存泄漏的源的标记。 为了加快符号解析，应指定模块名称 "nt"。 标记值必须以小字节序格式输入（即向后）。 由于池标记始终为四个字符，因此此标记实际上是一个-b-c--空间，而不只是 A-b-c。 因此，请使用以下命令：
    ```dbgcmd
    kd> ed nt!poolhittag ' cbA' 
    ```

3.  若要验证**PoolHitTag**的当前值，请使用[**Db （显示内存）**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令：
    ```dbgcmd
    kd> db nt!poolhittag L4 
    820f2ba4  41 62 63 20           Abc  
    ```

4.  每次分配或释放带有标记**Abc**的池时，调试器都会中断。 每次调试器在其中一项分配或自由操作上中断时，使用[**kb （显示 Stack Backtrace）**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)调试器命令来查看堆栈跟踪。

使用此过程，可以确定驻留在内存中的代码是带有标记**Abc**的 overallocating 池。

若要清除断点，请将**PoolHitTag**设置为零：

```dbgcmd
kd> ed nt!poolhittag 0 
```

如果有多个不同的位置正在分配带有此标记的内存，并且这些位置位于你编写的应用程序或驱动程序中，则可以更改你的源代码，以便为每个分配使用唯一标记。

如果您无法重新编译该程序，但您想要确定代码中的多个可能位置中的哪个位置导致了泄漏，则您可以 unassemble 每个位置的代码，并使用调试器编辑驻留在内存中的此代码，以便每个实例都使用 distinct （和以前未使用的）池标记。 然后允许系统运行几分钟或更多时间。 经过一段时间后，再次使用调试器中断，并使用[**！ poolfind**](-poolfind.md)扩展查找与每个新标记关联的所有池分配。

 

 





