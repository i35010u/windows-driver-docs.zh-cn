---
title: 缓存管理器支持例程
description: 缓存管理器支持例程
ms.assetid: 9ff905d9-8f85-4841-8bf5-437ccc3b3921
ms.date: 09/30/2019
ms.localizationpriority: medium
ms.openlocfilehash: d67eb197c8968c853ca21fc3ed35165d4eee45c0
ms.sourcegitcommit: c23a403b3ebea05bde96067b678a318ca9b0cabe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2019
ms.locfileid: "71955779"
---
# <a name="cache-manager-support-routines"></a>缓存管理器支持例程

内核模式文件系统和文件系统筛选器驱动程序可调用以下系统提供的缓存管理器函数和宏。 它们按字母顺序列出。

**头文件：** *ntifs*

**前缀： Cc * Xxx***

| 函数或宏 | 描述 |
| ----------------- | ----------- |
| **CcCanIWrite** | 确定调用方是否可以写入缓存文件。 |
| **CcCoherencyFlushAndPurgeCache** | 刷新和/或清除缓存以确保缓存的一致性。 |
| **CcCopyRead** | 将数据从缓存文件复制到用户缓冲区。 |
| **CcCopyReadEx** | 将数据从缓存文件复制到用户缓冲区。 操作的 i/o 字节计数将向发出线程收费。 |
| **CcCopyWrite** | 将数据从用户缓冲区复制到缓存文件。 |
| **CcCopyWriteEx** | 将数据从用户缓冲区复制到缓存文件。 操作的 i/o 字节计数将向发出线程收费。 |
| **CcCopyWriteWontFlush** | 确定在对**CcCopyWrite**的调用中要复制的数据量是否足够小，以便在调用**CcCopyWrite**并*等待*设置为**FALSE**时不需要立即刷新到磁盘。 |
| **CcDeferWrite** | 延迟写入缓存文件。 |
| **CcFastCopyRead** | 执行从缓存文件到内存中缓冲区的快速复制。 |
| **CcFastCopyWrite** | 执行从内存中的缓冲区写入缓存文件的快速复制。 |
| **CcFlushCache** | 将缓存文件的全部或一部分刷新到磁盘。
| **CcGetDirtyPages** | 搜索与给定日志句柄匹配的所有文件中的脏页。 |
| **CcGetFileObjectFromBcb** | 如果有一个指针指向某个文件的固定缓冲区控制块（BCB），则将返回一个指针，该指针指向缓存管理器为该文件使用的文件对象。 |
| **CcGetFileObjectFromSectionPtrs** | 如果有指向缓存文件的节对象指针的指针，则返回指向缓存管理器用于文件的文件对象的指针。 |
| **CcGetFileObjectFromSectionPtrsRef** | 当向缓存文件的 SECTION_OBJECT_POINTERS 结构传递指针时，将返回一个指针，该指针指向缓存管理器用于缓存文件的文件对象。 |
| **CcGetFileSizePointer** | 如果文件的文件对象有指针，则返回该文件的大小。 |
| **CcGetFlushedValidData** | 确定缓存文件中已刷新到磁盘的数量。 |
| **CcInitializeCacheMap** | 文件系统调用此例程来缓存文件。 |
| **CcIsFileCached** | 确定文件是否已缓存。 |
| **CcIsThereDirtyData** | 确定装入的卷是否包含系统缓存中有脏数据的任何文件。 |
| **CcIsThereDirtyDataEx** | 确定装入的卷是否包含系统缓存中包含已更新数据的任何文件，包括临时文件。 |
| **CcMapData** | 将缓存文件的指定字节范围映射到内存中的缓冲区。 |
| **CcPinMappedData** | 锁定缓存文件的指定字节范围。 |
| **CcPinRead** | 锁定缓存文件的指定字节范围，并将固定的数据读入内存中的缓冲区。 |
| **CcPreparePinWrite** | 为写入访问锁定缓存文件的指定字节范围。 |
| **CcPurgeCacheSection** | 清除系统缓存中的所有或部分缓存文件。 |
| **CcReadAhead** | 对缓存的文件执行预读（也称为 "延迟读取"）。 |
| **CcRemapBcb** | 将缓冲区控制块（BCB）附加时间映射到多个执行其他映射和取消固定的调用。 |
| **CcRepinBcb** | 将 BCB 额外固定一段时间，以防止通过对**CcUnpinData**的后续调用来释放它。 |
| **CcScheduleReadAhead** | 对缓存的文件执行预读（也称为 "延迟读取"）。 永远不应直接调用**CcScheduleReadAhead** ;改为调用**CcReadAhead** 。 |
| **CcScheduleReadAheadEx** | 对缓存的文件执行预读（也称为 "延迟读取"）。 操作的 i/o 字节计数按颁发线程收费。 |
| **CcSetAdditionalCacheAttributes** | 启用或禁用缓存文件上的预读（也称为 "延迟读取"）或写隐藏（也称为 "延迟写入"）。 |
| **CcSetAdditionalCacheAttributesEx** | 启用缓存文件上的扩展缓存行为。 |
| **CcSetBcbOwnerPointer** | 设置固定缓冲区控制块（BCB）的所有者线程指针。 |
| **CcSetDirtyPageThreshold** | 在缓存文件上设置每个文件脏页阈值。 |
| **CcSetDirtyPinnedData** | 将缓冲区控制块（BCB）标记为脏，其内容已修改。 |
| **CcSetFileSizes** | 为大小已更改的缓存文件更新缓存映射和节对象。 |
| **CcSetLogHandleForFile** | 设置文件的日志句柄。 |
| **CcSetReadAheadGranularity** | 为缓存的文件设置预读粒度。 |
| **CcUninitializeCacheMap** | 停止缓存文件的缓存。 |
| **CcUnpinData** | 释放先前调用**CcMapData**、 **CcPinRead**或**CcPreparePinWrite**映射或固定的缓存文件数据。 |
| **CcUnpinDataForThread** | 释放缓存文件的页，其缓冲区控制块（BCB）已被先前调用**CcSetBcbOwnerPointer**修改。 | **CcUnpinRepinnedBcb** | 取消固定被固定 buffer 控制块（BCB）。 |
| **CcWaitForCurrentLazyWriterActivity** | 将调用方置于等待状态，直到延迟写入器活动的当前批处理完成。 |
| **CcZeroData** | 为缓存或非缓存文件中指定范围的字节数。 |

以下**Cc * Xxx*** 例程提供用于传输到缓存的内存描述符列表（MDL）接口。 这些例程主要用于文件服务器。 其他任何人都应使用 FSRTL 和 FASTIO 接口。

| 函数 | 描述 |
| -------- | ----------- |
| **CcPrepareMdlWrite** | 提供对缓存的文件内存的直接访问，以便调用方可以将数据写入文件。 |
| **CcMdlRead** | 提供对缓存的文件内存的直接访问，以便调用方可以从文件读取数据。 |
| **CcMdlReadComplete** | 释放由**CcMdlRead**为缓存文件创建的 MDL。 |
| **CcMdlWriteAbort** | 释放由之前对 CcPrepareMdlWrite 的调用创建的 MDL **。** |
| **CcMdlWriteComplete** | 释放由**CcPrepareMdlWrite**为缓存文件创建的 MDL。 |
| **CcMdlRead** | 提供对缓存的文件内存的直接访问，以便调用方可以从文件读取数据。 |
