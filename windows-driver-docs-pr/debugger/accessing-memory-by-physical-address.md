---
title: 按物理地址访问内存
description: 按物理地址访问内存
keywords:
- 物理地址，访问内存
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecf71d628537754721a6126b0f6260b010d543c6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824367"
---
# <a name="accessing-memory-by-physical-address"></a>按物理地址访问内存


## <span id="ddk_debugging_bios_code_dbg"></span><span id="DDK_DEBUGGING_BIOS_CODE_DBG"></span>


若要读取物理地址，请使用 [**！ db**](-db---dc---dd---dp---dq---du---dw.md)， **！ dc**， **！ dd**， **！ dp**， **！ du**，！ **dw** 扩展命令。

若要写入物理地址，请使用 [**！ eb**](-eb---ed.md) 和 **！ ed** 扩展命令。

[**Fp (填充物理内存)**](f--fp--fill-memory-.md)命令将模式写入物理内存范围，请重复此模式直到范围已满。

在内核模式下使用 WinDbg 时，还可以从 " [内存" 窗口](memory-window.md)直接读取或写入物理内存。

若要在物理内存中搜索数据片段或数据范围，请使用 [**！ search**](-search.md) extension 命令。

此外，有关物理地址的详细信息，请参阅 [将虚拟地址转换为物理地址](converting-virtual-addresses-to-physical-addresses.md)。

 

 





