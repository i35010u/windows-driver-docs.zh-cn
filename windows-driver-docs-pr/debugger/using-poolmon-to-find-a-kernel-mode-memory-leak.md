---
title: 使用 PoolMon 查找内核模式内存泄漏
description: 使用 PoolMon 查找内核模式内存泄漏
ms.assetid: 383b5d9a-3e99-4dc5-bce9-bd44f2ef1dc0
keywords:
- 内存泄漏，内核模式下 PoolMon
- PoolMon
- PoolMon，查找内存泄漏
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 848b8e11bcd03bfa26161ff814dd034b3ffe8951
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544122"
---
# <a name="using-poolmon-to-find-a-kernel-mode-memory-leak"></a>使用 PoolMon 查找内核模式内存泄漏


如果您怀疑内核模式内存泄漏，以确定哪个池标记为泄漏与相关联的最简单方法是使用 PoolMon 工具。

PoolMon (Poolmon.exe) 监视器按池标记名称的池内存使用情况。 此工具包含 Windows Driver Kit (WDK) 中。 有关完整说明，请参阅[PoolMon](https://go.microsoft.com/fwlink/p/?linkid=122776) WDK 文档中。

### <a name="span-idenablepooltaggingwindows2000andwindowsxpspanspan-idenablepooltaggingwindows2000andwindowsxpspanenable-pool-tagging-windows-2000-and-windows-xp"></a><span id="enable_pool_tagging__windows_2000_and_windows_xp_"></span><span id="ENABLE_POOL_TAGGING__WINDOWS_2000_AND_WINDOWS_XP_"></span>启用池标记 （Windows 2000 和 Windows XP）

在 Windows 2000 和 Windows XP 首先必须使用 GFlags 启用池标记。 GFlags 包含在为 Windows 调试工具。 启动 GFlags、 选择**系统注册表**选项卡上，选中**启用池标记**框中，然后依次**应用**。 您必须重新启动 Windows 为此设置，才会生效。 有关更多详细信息，请参阅[GFlags](gflags.md)。

在 Windows Server 2003 和更高版本的 Windows 上，始终启用池标记。

### <a name="span-idusingpoolmonspanspan-idusingpoolmonspanusing-poolmon"></a><span id="using_poolmon"></span><span id="USING_POOLMON"></span>使用 PoolMon

PoolMon 标头显示总分页和非分页池字节数。 列显示为每个池标记的池中使用。 显示将自动更新每隔几秒。 例如：

```dbgcmd
Memory: 16224K Avail: 4564K PageFlts: 31 InRam Krnl: 684K P: 680K
Commit: 24140K Limit: 24952K Peak: 24932K Pool N: 744K P: 2180K

## Tag   Type  Allocs       Frees        Diff    Bytes       Per Alloc


CM    Paged   1283  ( 0)  1002  ( 0)   281  1377312   ( 0)  4901
Strg  Paged  10385 ( 10)  6658  ( 4)  3727   317952 ( 512)    85
Fat   Paged   6662  ( 8)  4971  ( 6)  1691   174560 ( 128)   103
MmSt  Paged    614  ( 0)   441  ( 0)   173    83456   ( 0)   482 
```

PoolMon 具有对根据各种条件的输出进行排序的命令键。 按每个命令，以便将数据重新排序与相关联的字母。 花费几秒钟时间来处理每个命令。

排序命令包括：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">命令键</th>
<th align="left">操作</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>P</strong></p></td>
<td align="left"><p>限制向非分页缓冲的池、 页面缓冲的池，或同时显示的标记。 重复按<strong>P</strong>循环通过每个选项，按该顺序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>B</strong></p></td>
<td align="left"><p>对标记排序最大字节使用情况。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>M</strong></p></td>
<td align="left"><p>最大字节分配对标记排序。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>T</strong></p></td>
<td align="left"><p>标记名称按字母顺序排列的标记。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>E</strong></p></td>
<td align="left"><p>将导致显示在底部包含分页和非分页总计。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>A</strong></p></td>
<td align="left"><p>对标记排序分配的大小。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>F</strong></p></td>
<td align="left"><p>对标记排序可用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>S</strong></p></td>
<td align="left"><p>对标记之间分配的差异进行排序，并释放。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Q</strong></p></td>
<td align="left"><p>退出 PoolMon。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idusingthepoolmonutilitytofindamemoryleakspanspan-idusingthepoolmonutilitytofindamemoryleakspanusing-the-poolmon-utility-to-find-a-memory-leak"></a><span id="using_the_poolmon_utility_to_find_a_memory_leak"></span><span id="USING_THE_POOLMON_UTILITY_TO_FIND_A_MEMORY_LEAK"></span>使用 PoolMon 实用程序以查找内存泄漏

若要查找内存泄漏 PoolMon 实用程序，请按照此过程操作：

1.  启动 PoolMon。

2.  如果已确定在非分页池发生泄漏，请按**P**一次; 如果已确定发生在页面缓冲池，请按**P**两次。 如果您不知道，不要按**P**以及包含这两种类型的池。

3.  按**B**以最大字节使用排序显示。

4.  启动测试。 拍摄屏幕快照并将其复制到记事本。

5.  需要一个新的屏幕截图半小时为单位。 通过比较屏幕截图，确定哪些标记的字节数不断增加。

6.  停止你的测试并等待几个小时。 在标记中有多少已释放了在此时间内？

通常情况下，应用程序达到一个稳定运行状态后，它会分配内存和可用内存大致相同的费率。 如果它往往不是将其释放更快地分配内存，内存使用量会随时间增加。 这通常指示内存泄漏。

### <a name="span-idaddressingtheleakspanspan-idaddressingtheleakspanaddressing-the-leak"></a><span id="addressing_the_leak"></span><span id="ADDRESSING_THE_LEAK"></span>寻址泄漏

确定哪个池标记为泄漏与相关联之后，这可能会显示所有需要了解有关泄漏。 如果您需要确定哪个特定的实例分配例程导致泄露，请参阅[使用内核调试器，以查找内核模式内存泄漏](using-the-kernel-debugger-to-find-a-kernel-mode-memory-leak.md)。

 

 





