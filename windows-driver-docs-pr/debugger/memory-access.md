---
title: 内存访问
description: 内存访问
ms.assetid: a5265f2c-61b9-4f0f-8cff-05da26010c6a
keywords:
- 调试器引擎，内存访问
- 内存访问
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3702792823bf2051abc3c6bbbb08fc1eea454696
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63384585"
---
# <a name="memory-access"></a>内存访问


## <span id="ddk_memory_access_dbx"></span><span id="DDK_MEMORY_ACCESS_DBX"></span>


若要直接读取和写入到目标的主内存、 寄存器以及其他数据空间的调试器引擎。

在用户模式下调试中，可以访问的虚拟内存和寄存器;不能访问的物理内存和其他数据空间。

引用在目标上的内存位置时，调试器引擎 API 始终使用 64 位地址。

如果目标使用 32 位地址，本机 32 位地址将自动进行符号扩展到 64 位地址引擎。 与目标进行通信时，该引擎将自动转换 64 位地址与本机 32 位地址之间。

本部分包括：

[虚拟和物理内存](virtual-and-physical-memory.md)

[注册](registers.md)

[其他数据空间](other-data-spaces.md)

 

 





