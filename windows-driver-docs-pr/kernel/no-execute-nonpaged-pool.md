---
title: 非执行 (NX) 非分页缓冲池
description: 作为最佳做法，Windows 8 及更高版本的 Windows 的驱动程序应从非执行 (NX) 非分页池分配其大部分或全部非分页内存。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 03f1c27da965918a316c49e4f454b443af35c0ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838007"
---
# <a name="no-execute-nx-nonpaged-pool"></a>非执行 (NX) 非分页缓冲池


作为最佳做法，Windows 8 及更高版本的 Windows 的驱动程序应从非执行 (NX) 非分页池分配其大部分或全部非分页内存。 通过从 NX 非分页池分配内存，内核模式驱动程序可防止恶意软件在此内存中执行指令，从而提高安全性。

从 Windows 8 开始，内核模式驱动程序可以从 NX 非分页内存池分配内存。 此池由一般用途的内核模式内存分配器进行管理，其操作方式类似于用户模式 Win32 堆分配器。 此池中的内存为 NX 和非分页。 X86、x64 和 ARM 处理器体系结构允许将内存页指定为 NX，以防止在这些页中执行指令。 通常，内核模式驱动程序使用从非分页池分配的内存来存储数据，而不需要在此内存中执行指令的能力。

## <a name="support-for-legacy-drivers"></a>对旧驱动程序的支持


在 Windows 7 和更早版本的 Windows 中，从非分页池分配的所有内存都是可执行的。 为了鼓励在 Windows 8 和更高版本的 Windows 中移植这些驱动程序以使用 NX 非分页池，Microsoft 提供了多种选择机制，使开发人员能够以最小的工作量更新其驱动程序。 有关详细信息，请参阅 [NX 池 Opt-In 机制](nx-pool-opt-in-mechanisms.md)。

为了向后兼容，在 windows 7 和更早版本的 Windows 上运行的驱动程序二进制文件和从可执行的非分页池分配内存的情况下，将在 Windows 8 和更高版本的 Windows 上运行，而不进行修改。 但是，这些驱动程序无法利用 NX 非分页池的增强安全性。

 

 




