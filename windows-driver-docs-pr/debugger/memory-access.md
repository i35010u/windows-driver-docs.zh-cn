---
title: 内存访问
description: 内存访问
ms.assetid: a5265f2c-61b9-4f0f-8cff-05da26010c6a
keywords:
- 调试器引擎，内存访问
- 内存访问
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 969be367161e337e595b88945c41ad21a447fe33
ms.sourcegitcommit: a44ade167cdfb541cf1818e9f9e3726f23f90b66
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2020
ms.locfileid: "94361359"
---
# <a name="memory-access"></a>内存访问


## <span id="ddk_memory_access_dbx"></span><span id="DDK_MEMORY_ACCESS_DBX"></span>


[调试器引擎](introduction.md#debugger-engine)提供直接从目标的主内存、寄存器和其他数据空间读取和向其写入数据的 *接口* 。

在用户模式调试中，只能访问虚拟内存和寄存器;物理内存和其他数据空间无法访问。

当引用目标上的内存位置时，调试器引擎 API 始终使用64位地址。

如果目标使用32位地址，则本机32位地址将自动由引擎对64位地址进行符号扩展。 与目标通信时，引擎将在64位地址和本机32位地址之间自动转换。

本节包括：

[虚拟和物理内存](virtual-and-physical-memory.md)

[寄存器](registers.md)

[其他数据空间](other-data-spaces.md)

 

 





