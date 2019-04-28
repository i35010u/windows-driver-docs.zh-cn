---
title: 内存
description: 内存
ms.assetid: 4aa5cf2b-e5f8-4358-b2cc-c677cd012f46
keywords:
- 调试器引擎内存
- 数据空间
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19bd486509ffd580b0be729cba51c670d39e0fca
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63334058"
---
# <a name="memory"></a>内存


[调试器引擎](introduction.md#debugger-engine)可以直接读取和写入目标的主内存、 寄存器以及其他数据空间。 在内核模式调试下的所有目标的内存均可用，包括虚拟内存、 物理内存、 寄存器、 模型特定注册 (MSRs)、 系统总线内存、 控制空间内存和 I/O： 内存。 在用户模式调试中，虚拟内存和寄存器都可用。

向客户端，使用 64 位地址的目标中的所有内存，引擎会公开。 如果目标使用 32 位地址与目标和客户端通信时，引擎将在根据需要自动 32 位和 64 位地址之间进行转换。 如果 32 位地址恢复目标-例如，通过读取来自内存或寄存器-它必须是符号扩展为 64 位然后调试器引擎 API 中使用它。 符号扩展来自动执行**ReadPointersVirtual**方法。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关读取和写入内存的详细信息，请参阅[内存访问](memory-access.md)。

 

 





