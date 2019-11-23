---
title: 单向和双向链接列表
description: 单向和双向链接列表
ms.assetid: 3a305f54-7866-4163-a3e4-e078d1927adc
keywords:
- 单向链接列表 WDK 内核
- 双重链接列表 WDK 内核
- 有序单向链接列表 WDK 内核
- SINGLE_LIST_ENTRY
- LIST_ENTRY
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: a9b545baa9f64be63e5778961a2d97a71a0187f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72836312"
---
# <a name="singly-and-doubly-linked-lists"></a>单向和双向链接列表





### <a name="singly-linked-lists"></a>单向链接列表

操作系统为使用[**单个\_列表\_条目**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_single_list_entry)结构的单个链接列表提供内置支持。 单个链接的列表包含一个列表头以及一些列表项。 （如果列表为空，则列表项的数目为零。）每个列表项都表示为**单个\_列表\_条目**结构。 List head 还表示为**单个\_列表\_条目**结构。

每个 **\_列表\_条目**结构包含一个指向另一个 **\_列表\_条目**结构的**下**一个成员。 在**单个\_列表中\_** 表示列表头的条目结构，**下一个**成员指向列表中的第一项，如果列表为空，则为 NULL。 在**单个\_列表中\_条目**结构，表示列表中的条目，**下一个**成员指向列表中的下一项，如果此项是列表中的最后一项，则为 NULL。

操作单向链接列表的例程采用指向[**单个\_列表\_项**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_single_list_entry)的指针，该列表表示列表头。 它们将更新**下一个**指针，使其指向操作后的列表的第一个条目。

假设*ListHead*变量是一个指针，指向表示列表头 **\_条目结构的单个\_列表**。 驱动程序操作*ListHead* ，如下所示：

-   若要将列表初始化为空，请将*ListHead * * *&gt;Next** 设置为**NULL**。

-   若要向列表中添加新项，请分配**单个\_列表\_项**以表示新项，然后调用[**PushEntryList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pushentrylist)将该项添加到列表的开头。

-   使用[**PopEntryList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-popentrylist)从列表中弹出第一项。

**单个\_列表\_条目**本身仅具有**下**一个成员。 若要将自己的数据存储在列表中，请将**单个\_列表\_条目**嵌入为描述列表项的结构的成员，如下所示。

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

若要向列表中添加新项，请将**XXX\_条目**结构，然后将指向**SingleListEntry**成员的指针传递到[**PushEntryList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-pushentrylist)。 若要将指向**单个\_列表\_项**的指针转换回**XXX\_项**，请使用[**包含\_记录**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)。 下面的示例说明了如何在单个链接列表中插入和删除驱动程序定义的条目。

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

系统还提供了 list 操作、 [**ExInterlockedPopEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545408)和[**ExInterlockedPushEntryList**](https://msdn.microsoft.com/library/windows/hardware/ff545418)的原子版本。 每个都采用附加的自旋锁参数。 例程在更新列表之前获取旋转锁，然后在操作完成后，例程释放自旋锁。 持有锁时，中断处于禁用状态。 对列表的每个操作都必须使用相同的自旋锁，以确保列表中的每个此类操作与所有其他操作同步。 只能将自旋锁用于这些**ExInterlocked*Xxx*列表**例程。 不要将自旋锁用于任何其他目的。 驱动程序可以对多个列表使用同一个锁，但这种行为会增加锁争用，因此驱动程序应避免出现此问题。

例如， **ExInterlockedPopEntryList**和**ExInterlockedPushEntryList**例程可以通过以 IRQL = 被动\_级别运行的驱动程序线程和 DIRQL 上运行的 ISR 来支持单个链接列表的共享。 这些例程在持有旋转锁时禁用中断。 因此，ISR 和 driver 线程可以安全地在其对这些**ExInterlocked*Xxx*列表**例程的调用中使用相同的自旋锁，而不会导致死锁。

不要在同一列表中混合对列表操作的原子和非原子版本的调用。 如果原子和非原子版本在同一列表上同时运行，则数据结构可能会损坏，计算机可能会停止响应或 bug 检查（即，*崩溃*）。 （在调用非原子例程时，无法获取旋转锁，因为这种方法可将调用混合到列表操作的原子和非原子版本。 不支持以这种方式使用旋转锁定，这可能仍会导致列表损坏。）

系统还提供了另一种更有效的原子单向链接列表实现。 有关详细信息，请参阅有[序单向链接列表](#sequenced-singly-linked-lists)。

### <a name="doubly-linked-lists"></a>双重链接列表

操作系统为使用[**LIST\_条目**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)结构的双重链接列表提供内置支持。 双重链接列表由列表头和一些列表项组成。 （如果列表为空，则列表项的数目为零。）每个列表项都表示为一个**列表\_条目**结构。 List head 还会表示为**列表\_条目**结构。

每个**列表\_条目**结构都包含一个**Flink**成员和一个**闪烁**成员。 这两个成员都是指向**列出\_条目**结构的指针。

在**列表中\_条目**结构表示列表头， **Flink**成员指向列表中的第一项，**闪烁**成员指向列表中的最后一项。 如果列表为空，则**Flink**并将列表头点**闪烁**到列表头本身。

在**列表中\_条目**结构（表示列表中的条目）， **Flink**成员指向列表中的下一项，**闪烁**成员指向列表中的上一项。 （如果项是列表中的最后一个，则**Flink**指向列表头。 同样，如果项是列表中的第一个项，则**闪烁**会指向列表头。）

（尽管这些规则乍一看看起来很奇怪，但它们允许列表插入和删除操作在没有条件代码分支的情况下实现。）

操作双重链接列表的例程采用指向[**列表\_项**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)的指针，该列表表示列表头。 这些例程将更新列表头中的**Flink**和**闪光**成员，使这些成员指向结果列表中的第一个和最后一个条目。

假设*ListHead*变量是一个指针，该指针指向表示列表标题的**列表\_条目**结构。 驱动程序操作*ListHead* ，如下所示：

-   若要将列表初始化为空，请使用[**InitializeListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-initializelisthead)，它将初始化*ListHead * * *-&gt;Flink** and *ListHead * * *-&gt;闪烁**，以指向*ListHead*。

-   若要在列表的开头插入新项，请分配一个**列表\_项**以表示新的项，然后调用[**InsertHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-insertheadlist)以将该项插入到列表的开头。

-   若要将新项追加到列表的尾部，请分配一个**列表\_项**来表示新项，然后调用[**InsertTailList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-inserttaillist)将该项插入到列表的末尾。

-   若要从列表中删除第一项，请使用[**RemoveHeadList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeheadlist)。 这会返回指向列表中已删除条目的指针，如果列表为空，则返回*ListHead* 。

-   若要从列表中删除最后一项，请使用[**RemoveTailList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removetaillist)。 这会返回指向列表中已删除条目的指针，如果列表为空，则返回*ListHead* 。

-   若要从列表中删除指定的条目，请使用[**RemoveEntryList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-removeentrylist)。

-   若要查看列表是否为空，请使用[**IsListEmpty**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-islistempty)。

-   若要将列表附加到另一个列表的尾部，请使用[**AppendTailList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-appendtaillist)。

[ **\_条目的列表**](https://docs.microsoft.com/windows/desktop/api/ntdef/ns-ntdef-_list_entry)本身只包含**闪烁**和**Flink**的成员。 若要将自己的数据存储在列表中，请将**列表\_项**嵌入为描述列表项的结构的成员，如下所示。

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

若要向列表中添加新条目，请将**XXX\_条目**结构，然后将指向**ListEntry**成员的指针传递到**InsertHeadList**或**InsertTailList**。 若要将指向**列表\_项**的指针转换回**XXX\_条目**，请使用[**包含\_记录**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)。 有关此技术的示例，请参阅上面的单独链接列表。

系统还提供了 list 操作、 [**ExInterlockedInsertHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545397)、 [**ExInterlockedInsertTailList**](https://msdn.microsoft.com/library/windows/hardware/ff545402)和[**ExInterlockedRemoveHeadList**](https://msdn.microsoft.com/library/windows/hardware/ff545427)的原子版本。 （请注意，没有**RemoveTailList**或**RemoveEntryList**的原子版本。）每个例程使用额外的自旋锁参数。 例程在更新列表之前获取旋转锁，然后在操作完成后释放自旋锁。 持有锁时，中断处于禁用状态。 列表上的每个操作都必须使用相同的自旋锁来确保列表中的每个此类操作相互同步。 只能将自旋锁用于这些**ExInterlocked*Xxx*列表**例程。 不要将自旋锁用于任何其他目的。 驱动程序可以对多个列表使用同一个锁，但这种行为会增加锁争用，因此驱动程序应避免出现此问题。

例如， **ExInterlockedInsertHeadList**、 **ExInterlockedInsertTailList**和**EXINTERLOCKEDREMOVEHEADLIST**例程可以通过以 IRQL = 被动\_级别运行的驱动程序线程和在 DIRQL 运行的 ISR 来支持双重链接列表的共享。 这些例程在持有旋转锁时禁用中断。 因此，ISR 和 driver 线程可以安全地在其对这些**ExInterlocked*Xxx*列表**例程的调用中使用相同的自旋锁，而不会导致死锁。

不要在同一列表中混合对列表操作的原子和非原子版本的调用。 如果原子和非原子版本在同一列表上同时运行，则数据结构可能会损坏，并且计算机可能会停止响应或 bug 检查（即，*崩溃*）。 （在调用非原子例程时无法获取旋转锁，以避免混合对列表操作的原子和非原子版本的调用。 不支持以这种方式使用旋转锁定，这可能仍会导致列表损坏。）

### <a name="sequenced-singly-linked-lists"></a>有序单向链接列表

排序的单向链接列表是支持原子操作的单个链接列表的实现。 与[单独](#singly-linked-lists)链接列表中所述的单个链接列表的实现相比，原子操作更高效。

[**SLIST\_标头**](https://docs.microsoft.com/windows-hardware/drivers/kernel/eprocess)结构用于描述序列化的单向链接列表的头，而[**SLIST\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_slist_entry)用于描述列表中的条目。

驱动程序按如下方式操作列表：

-   若要初始化**SLIST\_标头**结构，请使用[**ExInitializeSListHead**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-initializeslisthead)。

-   若要向列表中添加新项，请分配**SLIST\_项**来表示新项，然后调用[**ExInterlockedPushEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpushentryslist)将该项添加到列表的开头。

-   使用[**ExInterlockedPopEntrySList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedpopentryslist)从列表中弹出第一项。

-   若要完全清除列表，请使用[**ExInterlockedFlushSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exinterlockedflushslist)。

-   若要确定列表中的条目数，请使用[**ExQueryDepthSList**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-exquerydepthslist)。

[**SLIST\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_slist_entry)本身仅具有**下**一个成员。 若要将自己的数据存储在列表中，请将**SLIST\_项**嵌入为描述列表项的结构的成员，如下所示。

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

若要向列表中添加新项，请将**XXX\_条目**结构，然后将指向**SListEntry**成员的指针传递到**ExInterlockedPushEntrySList**。 若要将指向**SLIST\_项**的指针转换回**XXX\_条目**，请使用[**包含\_记录**](https://docs.microsoft.com/windows-hardware/drivers/kernel/mm-bad-pointer)。 有关此技术的示例，请参阅[单独链接列表](#singly-linked-lists)。

**警告**   对于64位 Microsoft Windows 操作系统， [**SLIST\_条目**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_slist_entry)结构必须是16字节对齐的。

 

Windows XP 和更高版本的 Windows 提供了在 Windows 2000 中不可用的已排序单向链接列表函数的优化版本。 如果驱动程序使用这些功能，并且还必须使用 Windows 2000 运行，则驱动程序必须定义 \_WIN2K\_兼容性\_SLIST\_用法标志，如下所示：

```cpp
#define _WIN2K_COMPAT_SLIST_USAGE
```

对于基于 x86 的处理器，此标志将导致编译器使用与 Windows 2000 兼容的已排序单向链接列表函数版本。

 

 




