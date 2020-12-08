---
title: 内存
description: 内存
keywords:
- 调试器引擎，内存
- 数据空间
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7fb25ab953bbf154942050e54415b50830d9eb55
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828885"
---
# <a name="memory"></a>内存


[调试器引擎](introduction.md#debugger-engine)可以直接读取和写入目标的主内存、寄存器和其他数据空间。 在内核模式调试中，目标的所有内存都可用，包括虚拟内存、物理内存、寄存器、特定于模型的寄存器 (MSRs) 、系统总线内存、Control-Space 内存和 i/o 内存。 在用户模式调试中，仅可用虚拟内存和注册。

引擎使用64位地址向客户端公开目标中的所有内存。 如果目标使用32位地址，当与目标和客户端通信时，引擎将根据需要自动在32位和64位地址之间转换。 如果从目标恢复32位地址（例如，通过读取内存或注册），则必须先将其标记为64位，然后才能将其用于调试器引擎 API。 签名扩展由 **ReadPointersVirtual** 方法自动执行。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关读取和写入内存的详细信息，请参阅 [内存访问](memory-access.md)。

 

 





