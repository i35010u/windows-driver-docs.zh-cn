---
title: 无执行 (NX) 非分页缓冲的池
description: 最佳做法是，Windows 8 和更高版本的 Windows 驱动程序应从中分配大多数或所有其非分页内存不执行 (NX) 非分页缓冲的池。
ms.assetid: E5BF34F6-ABA0-4EC7-B740-CC83EF8438CF
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0981ffff9c53307c3d39958990c585e529b436e9
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522927"
---
# <a name="no-execute-nx-nonpaged-pool"></a>无执行 (NX) 非分页缓冲的池


最佳做法是，Windows 8 和更高版本的 Windows 驱动程序应从中分配大多数或所有其非分页内存不执行 (NX) 非分页缓冲的池。 通过从 NX 中分配内存，非分页的池的内核模式驱动程序提高了安全性通过防止恶意软件执行此内存中的说明。

从 Windows 8 开始，内核模式驱动程序可以分配的内存从 NX 池非分页的内存。 为用户模式 Win32 堆分配器的运行方式类似的多用途的内核模式内存分配器管理此池。 此池中的内存是 NX 和非分页。 X86、 x64 和 ARM 处理器体系结构使被指定为 NX 以防止这些页面中的说明执行的内存页。 通常情况下，内核模式驱动程序使用从非分页缓冲池分配的内存来存储数据，并且不需要执行此内存中的说明的功能。

## <a name="support-for-legacy-drivers"></a>对旧版驱动程序的支持


在 Windows 7 和 Windows 的早期版本中，从非分页缓冲池分配的所有内存都是可执行文件。 为了鼓励移植这些驱动程序以使用 NX 的 Windows 8 和更高版本的 Windows，Microsoft 中的非分页缓冲的池提供了几种选择机制，使开发人员能够轻松地更新其驱动程序。 有关详细信息，请参阅[NX 池选择的机制](nx-pool-opt-in-mechanisms.md)。

为了向后兼容，驱动程序二进制文件，运行在 Windows 7 和早期版本的 Windows，并从可执行文件的非分页池分配内存将运行 Windows 8 和更高版本的 Windows，而无需修改。 但是，这些驱动程序不利用改进的安全性的 NX 非分页缓冲的池。

 

 




