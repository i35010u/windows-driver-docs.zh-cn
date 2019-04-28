---
title: CLFS 封送区域
description: CLFS 封送区域
ms.assetid: 1153bcfd-43e9-43bd-b893-5ec044ea9584
keywords:
- 常见日志文件系统 WDK 内核，封送处理区域
- CLFS WDK 内核，封送处理区域
- 封送处理区域 WDK CLFS
- 日志 I/O 缓冲区 WDK CLFS
- 缓冲区 WDK CLFS 的日志 I/O 的最大数量
- WDK CLFS 的内存分配
- 缓冲区 WDK CLFS
- 追加记录 WDK CLFS
- 稳定的存储 WDK CLFS
- 易失性内存 WDK CLFS
- 存储 WDK CLFS
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6202c5524e84a9bb4239c866643c694809d5f9d7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343711"
---
# <a name="clfs-marshalling-areas"></a>CLFS 封送区域





公用日志文件系统 (CLFS) 客户端将追加到日志记录[*封送处理区域*](clfs-terminology.md#kernel-clfs-term-marshalling-area)易失性内存中和 CLFS 会定期将写入到稳定存储这些记录。 封送处理区域是日志 I/O 缓冲区，其中每个可容纳多个日志记录的集合。 日志 I/O 缓冲区保留记录最近已写入流 （但可能不会刷新到稳定存储） 以及最近已从流中读取的记录。

通过调用创建封送处理区域[ **ClfsCreateMarshallingArea**](https://msdn.microsoft.com/library/windows/hardware/ff541520)，必须指定大小的日志 I/O 缓冲区时封送处理区域将使用，并且这些缓冲区中为是否分页或非页面缓冲池。 封送处理区域中的所有日志 I/O 缓冲区都都具有相同的大小，并 CLFS 确保大小是基础的稳定存储媒体上的扇区大小的倍数。 也就是说，CLFS 采用你请求的大小，并将它向上舍入为使 I/O 缓冲区与稳定的存储介质兼容所需。

CLFS 分配并释放日志 I/O 缓冲区根据需要但必须选择设置可以一次分配的 I/O 缓冲区的最大数目。 此外可以提供自己的缓冲区分配和释放函数。

若要指定可用于写入日志记录一次分配的日志 I/O 缓冲区的最大数目，设置*cMaxWriteBuffers*的参数**ClfsCreateMarshallingArea**函数。 限制的缓冲区数会影响到稳定存储; 的刷新频率使用较少的缓冲区，日志记录必须写入到稳定存储更频繁。 如果不需要控制刷新频率，设置*cMaxWriteBuffers*为 INFINITE （在 Winbase.h 中定义）。

若要指定可以用于读取日志记录一次分配的日志 I/O 缓冲区的最大数目，设置*cMaxReadBuffers*的参数**ClfsCreateMarshallingArea**函数。 如果不需要控制分配的读取缓冲区的数量，设置*cMaxReadBuffers*为 INFINITE。

如果你想要执行自己的日志 I/O 缓冲区的内存分配，设置*pfnAllocBuffer*并*pfnFreeBuffer*的参数**ClfsCreateMarshallingArea**函数使其指向您自己的分配和释放函数。 然后 CLFS 将调用函数来执行实际的内存分配和解除分配，需要创建或释放日志 I/O 缓冲区时。

在某些情况下，你可能想要提前封送处理区域中保留的空间。 例如，您可能知道要编写的一组 10 个日志记录，并且你想要确保在整个集的封送处理区域没有足够的空间。 若要保留十个记录的空间，创建包含记录的大小的 10 个元素数组，然后将传递到的数组[ **ClfsReserveAndAppendLog** ](https://msdn.microsoft.com/library/windows/hardware/ff541723)函数，在*rgcbReservation*参数。 **ClfsReserveAndAppendLog**是一个多用途函数，封送处理区域中保留了空间或将日志记录追加到流或以原子方式做到这这些内容。 通过适当地设置参数，你可以调用**ClfsReserveAndAppendLog**而无需实际追加到流的任何记录保留供将来使用的空间。

 

 




