---
title: 查看和编辑内存中 KD
description: 查看和编辑内存中 KD
ms.assetid: 7E40F32F-C7B4-44A2-B3F9-84D673013EB2
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e5f10729960d63ee57d570f4ead32ab083cc2a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526296"
---
# <a name="viewing-and-editing-memory-in-kd"></a>查看和编辑内存中 KD


## <a name="span-idviewingandeditingmemoryspanspan-idviewingandeditingmemoryspanspan-idviewingandeditingmemoryspanviewing-and-editing-memory"></a><span id="Viewing_and_Editing_Memory"></span><span id="viewing_and_editing_memory"></span><span id="VIEWING_AND_EDITING_MEMORY"></span>查看和编辑内存


KD，您可以查看和编辑通过输入的一个内存[**显示内存**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令，并且您可以通过输入之一来编辑内存[**输入值**](e--ea--eb--ed--ed--ef--ep--eq--eu--ew--eza--ezu--enter-values-.md)命令。 这些命令的详细讨论，请参阅[访问虚拟地址的内存](accessing-memory-by-virtual-address.md)并[访问内存的物理地址](accessing-memory-by-physical-address.md)。

## <a name="span-idviewingandeditingvariablesspanspan-idviewingandeditingvariablesspanspan-idviewingandeditingvariablesspanviewing-and-editing-variables"></a><span id="Viewing_and_Editing_Variables"></span><span id="viewing_and_editing_variables"></span><span id="VIEWING_AND_EDITING_VARIABLES"></span>查看和编辑变量


KD，可以查看和编辑通过输入命令的全局变量。 调试器将解释为一个虚拟地址的全局变量的名称。 因此，所有命令中所述[访问内存的虚拟地址](accessing-memory-by-virtual-address.md)可用于读取或写入全局变量。 有关查看和编辑全局变量的其他信息，请参阅[访问全局变量](accessing-global-variables.md)。

KD 可以查看和编辑通过输入命令的本地变量。 调试器将解释为一个地址的本地变量的名称。 因此，所有命令中所述[访问内存的虚拟地址](accessing-memory-by-virtual-address.md)可用于读取或写入本地变量。 但是，如果有必要向符号是本地命令指示前, 加上美元符号 （$） 和符号感叹号 （！ )，如`$!var`。 有关查看和编辑本地变量的其他信息，请参阅[访问本地变量](accessing-local-variables.md)。

 

 





