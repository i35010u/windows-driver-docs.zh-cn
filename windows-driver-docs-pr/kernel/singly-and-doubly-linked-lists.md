---
title: 单向和双向链接列表
description: 单向和双向链接列表
ms.assetid: 3a305f54-7866-4163-a3e4-e078d1927adc
keywords:
- 单向链接的列表 WDK 内核
- 双向链接的列表 WDK 内核
- 已编序的单向链接的列表 WDK 内核
- SINGLE_LIST_ENTRY
- LIST_ENTRY
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0b8358c4a7fc3f5add12e80bfda98a0a5d00e76
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383017"
---
# <a name="singly-and-doubly-linked-lists"></a>单向和双向链接列表





### <a name="singly-linked-lists"></a>单独链接的列表

操作系统使用的单向链接列表提供内置支持[**单个\_列表\_条目**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_single_list_entry)结构。 单向链接的列表包括列表头以及一定数量的列表项。 （列表项数为零如果列表为空。）每个列表项都表示为**单个\_列表\_条目**结构。 列表头也表示为**单个\_列表\_条目**结构。

每个**单个\_列表\_条目**结构包含**下一步**指向另一个的成员**单一\_列表\_条目**结构。 在中**单个\_列表\_条目**结构，它表示列表头**下一步**成员指向的第一项在列表中，或为 NULL，如果列表为空。 在中**单个\_列表\_条目**结构，它表示在列表中，一个条目**下一步**成员指向下一个条目的列表中，或如果此条目中的最后一个，则为 NULL列表。

操作的单向链接的列表的例程将指针指向[**单个\_列表\_条目**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_single_list_entry) ，表示列表头。 他们更新**下一步**指针使其指向列表的第一个条目，操作完成后。

假设*ListHead*变量是一个指向**单个\_列表\_条目**结构，它表示列表头。 驱动程序操作*ListHead* ，如下所示：

-   若要初始化为空列表，请设置*ListHead * * *-&gt;下一步** 要**NULL**。

-   若要将新条目添加到列表中，分配**单个\_列表\_条目**以表示新的条目，然后调用[ **PushEntryList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pushentrylist)添加到列表的开头的条目。

-   通过使用 pop 在列表外的第一个条目[ **PopEntryList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-popentrylist)。

一个**单个\_列表\_条目**，其本身而言，只有**下一步**成员。 若要将你自己的数据存储在列表中，嵌入**单个\_列表\_条目**作为描述列表项，按如下所示的结构的成员。

```cpp
typedef struct {
  // driver-defined members
  .
  .
  .
  SINGLE_LIST_ENTRY SingleListEntry;
 
  // other driver-defined members
  .
  .
  .
} XXX_ENTRY;
```

若要将新条目添加到列表中，分配**XXX\_条目**结构，，然后将传递一个指向**SingleListEntry**成员添加到[ **PushEntryList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-pushentrylist). 要转换的指针**单个\_列表\_条目**回**XXX\_条目**，使用[**内含\_记录**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)。 下面是示例的例程的插入和从单向链接列表中删除驱动程序定义的项。

```cpp
typedef struct {
  PVOID DriverData1;
  SINGLE_LIST_ENTRY SingleListEntry;
  ULONG DriverData2;
} XXX_ENTRY, *PXXX_ENTRY;

void
PushXxxEntry(PSINGLE_LIST_ENTRY ListHead, PXXX_ENTRY Entry)
{
    PushEntryList(ListHead, &(Entry->SingleListEntry));
}

PXXX_ENTRY
PopXxxEntry(PSINGLE_LIST_ENTRY ListHead)
{
    PSINGLE_LIST_ENTRY SingleListEntry;
    SingleListEntry = PopEntryList(ListHead);
    return CONTAINING_RECORD(SingleListEntry, XXX_ENTRY, SingleListEntry);
}
```

系统还提供了原子版本的列表操作[ **ExInterlockedPopEntryList** ](https://msdn.microsoft.com/library/windows/hardware/ff545408)并[ **ExInterlockedPushEntryList** ](https://msdn.microsoft.com/library/windows/hardware/ff545418). 每个都采用一个其他数值调节钮锁参数。 例程自旋锁之前获取它将更新列表中，而该例程然后在操作完成后释放自旋锁。 持有锁，而将禁用中断。 列表上的每个操作必须使用相同的旋转锁来确保每个此类操作列表上的同步与每个其他操作。 必须仅使用这些使用旋转锁**ExInterlocked*Xxx*列表**例程。 请不要用于任何其他用途的自旋锁。 驱动程序可用于多个列表的同一个锁，但此行为加剧锁争用情况，因此，驱动程序应避免它。

例如， **ExInterlockedPopEntryList**并**ExInterlockedPushEntryList**例程可以支持在 IRQL 运行驱动程序线程共享的单向链接列表 = 被动\_级别和在 DIRQL 运行 ISR。 数值调节钮锁时，这些例程会禁用中断。 因此，ISR 和驱动程序线程可以安全地使用相同的旋转锁在其调用中对这些**ExInterlocked*Xxx*列表**而且不会发生死锁的例程。

不要混合对该列表的列表操作的原子和非原子版本的调用。 如果原子和非原子版本相同的列表上同时运行，可能会损坏数据结构和计算机可能停止响应或错误检查 (即*崩溃*)。 （不能调用作为混合对原子和非原子版本的列表操作的调用的替代方法的非原子例程时获取的自旋锁。 旋转锁中使用这种方式不受支持且可能仍会导致列表损坏。）

系统还提供更高效的其他实现原子单独链接的列表。 有关详细信息，请参阅[已排序的单向链接列出了](#sequenced-singly-linked-lists)。

### <a name="doubly-linked-lists"></a>双向链接的列表

操作系统使用的双向链接列表提供内置支持[**列表\_条目**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)结构。 双向链接的列表包括列表头以及一定数量的列表项。 （列表项数为零如果列表为空。）每个列表项都表示为**列表\_条目**结构。 列表头也表示为**列表\_条目**结构。

每个**列表\_条目**结构中包含**Flink**成员和一个**闪烁**成员。 这两个成员都是指向**列表\_条目**结构。

在**列表\_条目**结构，它表示列表头**Flink**成员将指向列表中的第一个条目并**闪烁**成员将指向在列表中的最后一个条目。 如果列表为空，则**Flink**并**闪烁**列表头指向列表的头本身。

在中**列表\_条目**结构，它表示在列表中，一个条目**Flink**成员将指向下一个条目在列表中，和**闪烁**成员点在列表中的上一项。 (如果项是在列表中，最后一个**Flink**指向列表头。 同样，如果项是在列表中，第一个**闪烁**指向列表头。)

（虽然这些规则可能乍一看有点令人惊讶，它们允许列表来实现与没有条件代码分支的插入和删除操作。）

处理双向链接的列表的例程将指针指向[**列表\_条目**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry) ，表示列表头。 这些例程更新**Flink**并**闪烁**列表中的成员头，使这些成员指向生成的列表中的第一个和最后一个条目。

假设*ListHead*变量是一个指向**列表\_条目**结构，它表示列表头。 驱动程序操作*ListHead* ，如下所示：

-   若要初始化为空列表，请使用[ **InitializeListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-initializelisthead)，哪些初始化*ListHead * * *-&gt;Flink** 和*ListHead * * *-&gt;闪烁** 以指向*ListHead*。

-   若要在列表的开头处插入新条目，分配**列表\_条目**以表示新的条目，然后调用[ **InsertHeadList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-insertheadlist)插入处的项列表的开头。

-   若要将新条目追加到列表的结尾，分配**列表\_条目**以表示新的条目，然后调用[ **InsertTailList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-inserttaillist)插入处的项列表的末尾。

-   若要从列表中删除第一个条目，请使用[ **RemoveHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-removeheadlist)。 这对已删除的条目返回一个指针，或从列表中， *ListHead*如果列表为空。

-   若要从列表中删除最后一个条目，请使用[ **RemoveTailList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-removetaillist)。 这对已删除的条目返回一个指针，或从列表中， *ListHead*如果列表为空。

-   若要从列表中删除指定的项，请使用[ **RemoveEntryList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-removeentrylist)。

-   若要查看是否为空列表，请使用[ **IsListEmpty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-islistempty)。

-   若要追加到另一个列表的结尾的列表，请使用[ **AppendTailList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-appendtaillist)。

一个[**列表\_条目**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)，其本身而言，只有**闪烁**并**Flink**成员。 若要将你自己的数据存储在列表中，嵌入**列表\_条目**作为描述列表项，按如下所示的结构的成员。

```cpp
typedef struct {
  // driver-defined members
  .
  .
  .
  LIST_ENTRY ListEntry;
 
  // other driver-defined members.
  .
  .
  .
} XXX_ENTRY;
```

若要将新条目添加到列表中，分配**XXX\_条目**结构，，然后将传递一个指向**ListEntry**成员添加到**InsertHeadList**或**InsertTailList**。 要转换的指针**列表\_条目**回**XXX\_条目**，使用[**内含\_记录**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer). 有关此技术的示例，使用单向链接列表，请参阅单向链接列表更高版本。

系统还提供了原子版本的列表操作[ **ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)， [ **ExInterlockedInsertTailList** ](https://msdn.microsoft.com/library/windows/hardware/ff545402)，并[ **ExInterlockedRemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545427)。 (请注意，有没有原子版本**RemoveTailList**或**RemoveEntryList**。)每个例程需要一个其他数值调节钮锁参数。 例程获取更新的列表之前自旋锁，然后在操作完成后释放自旋锁。 持有锁，而将禁用中断。 在列表上的每个操作必须使用相同的旋转锁来确保与每个其他同步列表上的每个此类操作。 必须仅使用这些使用旋转锁**ExInterlocked*Xxx*列表**例程。 请不要用于任何其他用途的自旋锁。 驱动程序可用于多个列表的同一个锁，但此行为加剧锁争用情况，因此，驱动程序应避免它。

例如， **ExInterlockedInsertHeadList**， **ExInterlockedInsertTailList**，并**ExInterlockedRemoveHeadList**例程可以支持共享的双向链接的列表由驱动程序线程运行在 IRQL = 被动\_级别和运行在 DIRQL ISR。 数值调节钮锁时，这些例程会禁用中断。 因此，ISR 和驱动程序线程可以安全地使用相同的旋转锁在其调用中对这些**ExInterlocked*Xxx*列表**而且不会发生死锁的例程。

不要混合对该列表的列表操作的原子和非原子版本的调用。 如果原子和非原子版本相同的列表上同时运行，数据结构可能会损坏，计算机可能停止响应或错误检查 (即*崩溃*)。 (您不能处理调用的非原子例程，若要避免混合对原子和非原子版本的列表操作的调用时获取自旋锁。 旋转锁中使用这种方式不受支持且可能仍会导致列表损坏。）

### <a name="sequenced-singly-linked-lists"></a>已编序的单向链接的列表

已编序的单向链接的列表是支持原子操作的单向链接列表实现。 它是原子操作比单独链接的列表中所述的实现更高效[单向链接列表](#singly-linked-lists)。

[ **SLIST\_标头**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构用于描述已编序的单向链接列表中，头时[ **SLIST\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_slist_entry)用于描述列表中的条目。

驱动程序操作列表，如下所示：

-   若要初始化**SLIST\_标头**结构，请使用[ **ExInitializeSListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-initializeslisthead)。

-   若要将新条目添加到列表中，分配**SLIST\_条目**以表示新的条目，然后调用[ **ExInterlockedPushEntrySList** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinterlockedpushentryslist)要添加到项列表的开头。

-   通过使用 pop 在列表外的第一个条目[ **ExInterlockedPopEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinterlockedpopentryslist)。

-   若要完全清除列表，请使用[ **ExInterlockedFlushSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exinterlockedflushslist)。

-   若要确定列表中的条目数，请使用[ **ExQueryDepthSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-exquerydepthslist)。

一个[ **SLIST\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_slist_entry)，其本身而言，只有**下一步**成员。 若要将你自己的数据存储在列表中，嵌入**SLIST\_条目**作为描述列表项，按如下所示的结构的成员。

```cpp
typedef struct 
{
  // driver-defined members
  .
  .
  .
  SLIST_ENTRY SListEntry;
  // other driver-defined members
  .
  .
  .

} XXX_ENTRY;
```

若要将新条目添加到列表中，分配**XXX\_条目**结构，，然后将传递一个指向**SListEntry**成员添加到**ExInterlockedPushEntrySList**. 要转换的指针**SLIST\_条目**回**XXX\_条目**，使用[**内含\_记录**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer). 有关此技术，单独使用非序列化的示例链接列表，请参阅[单向链接列表](#singly-linked-lists)。

**警告**  于 64 位 Microsoft Windows 操作系统[ **SLIST\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_slist_entry)结构必须是 16 字节对齐。

 

Windows XP 和更高版本的 Windows 提供了在 Windows 2000 中不可用的已编序的单向链接的列表函数的优化的版本。 如果您的驱动程序使用这些函数，并且也必须运行 Windows 2000，驱动程序必须定义\_WIN2K\_兼容性\_SLIST\_用法标志，如下所示：

```cpp
#define _WIN2K_COMPAT_SLIST_USAGE
```

对于基于 x86 的处理器，此标志会导致编译器使用已编序的单向链接的列表函数与 Windows 2000 兼容的版本。

 

 




