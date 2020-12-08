---
title: 在 CDB 中查看和编辑内存
description: 在 CDB 中查看和编辑内存
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6432d9f35eaec578459f9faba9f255d1014296f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787713"
---
# <a name="viewing-and-editing-memory-in-cdb"></a>在 CDB 中查看和编辑内存


## <a name="span-idviewing_and_editing_memoryspanspan-idviewing_and_editing_memoryspanspan-idviewing_and_editing_memoryspanviewing-and-editing-memory"></a><span id="Viewing_and_Editing_Memory"></span><span id="viewing_and_editing_memory"></span><span id="VIEWING_AND_EDITING_MEMORY"></span>查看和编辑内存


在 CDB 中，可以通过输入 " [**显示内存**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md) " 命令来查看和编辑内存，还可以通过输入 " [**输入值**](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md) " 命令之一来编辑内存。 有关这些命令的详细讨论，请参阅 [按虚拟地址访问内存](accessing-memory-by-virtual-address.md) 和 [通过物理地址访问内存](accessing-memory-by-physical-address.md)。

## <a name="span-idviewing_and_editing_variablesspanspan-idviewing_and_editing_variablesspanspan-idviewing_and_editing_variablesspanviewing-and-editing-variables"></a><span id="Viewing_and_Editing_Variables"></span><span id="viewing_and_editing_variables"></span><span id="VIEWING_AND_EDITING_VARIABLES"></span>查看和编辑变量


在 CDB 中，可以通过输入命令来查看和编辑全局变量。 调试器将全局变量的名称解释为虚拟地址。 因此，在 [按虚拟地址访问内存](accessing-memory-by-virtual-address.md) 中所述的所有命令都可用于读取或写入全局变量。 有关查看和编辑全局变量的其他信息，请参阅 [访问全局变量](accessing-global-variables.md)。

在 CDB 中，可以通过输入命令来查看和编辑局部变量。 调试器将本地变量的名称解释为地址。 因此，在 [按虚拟地址访问内存](accessing-memory-by-virtual-address.md) 中所述的所有命令都可用于读取或写入局部变量。 但是，如果需要指出某个符号为本地的命令，则在该符号前面加上一个美元符号 ( $ ) 并 ( 惊叹号！ ) ，如中所示 `$!var` 。 有关查看和编辑局部变量的其他信息，请参阅 [访问局部变量](accessing-local-variables.md)。

 

 





