---
title: 访问内存的物理地址
description: 访问内存的物理地址
ms.assetid: 248871dc-dac0-413e-8971-2ee2c2fe5290
keywords:
- 访问内存的物理地址
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21c56460649584f009fd49636646ea3620fa3380
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554864"
---
# <a name="accessing-memory-by-physical-address"></a>访问内存的物理地址


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


若要读取的物理地址，请使用[ **！ db**](-db---dc---dd---dp---dq---du---dw.md)， **！ dc**， **！ dd**， **！ dp**， **！ du**，并 **！ dw**扩展命令。

若要写入的物理地址，请使用[ **！ eb** ](-eb---ed.md)并 **！ ed**扩展命令。

[ **Fp （填充物理内存）** ](f--fp--fill-memory-.md)命令写入到的物理内存范围，一种模式写下去，直到该区域已满。

当您使用 WinDbg 在内核模式下时，还可以读取或写入到直接从物理内存[内存窗口](memory-window.md)。

若要搜索的一段数据或一系列数据的物理内存，请使用[ **！ 搜索**](-search.md)扩展命令。

此外，有关物理地址的详细信息，请参阅[转换到物理地址的虚拟地址](converting-virtual-addresses-to-physical-addresses.md)。

 

 





