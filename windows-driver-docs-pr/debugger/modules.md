---
title: 模块
description: 模块
ms.assetid: 0cd99869-4014-4f9f-b5f1-d06c69fd134e
keywords:
- 符号、模块
- 模块
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e1f8e0597ddfe35caccfcc41f569c17c05ce899
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72834336"
---
# <a name="modules"></a>模块


## <span id="modules"></span><span id="MODULES"></span>


*映像*是 Windows 已作为用户模式进程或内核的一部分加载的可执行文件、DLL 或驱动程序。 从中加载映像的文件称为其*映像文件*。

[调试器引擎](introduction.md#debugger-engine)缓存每个进程（或内核模式下的虚拟进程）的*模块*列表。 通常，此列表中的每个模块都表示进程中的一个映像。 该引擎的模块列表可以使用**reload.sql**与目标同步。

**注意**   内核模式调试中，此虚拟进程的引擎模块列表同时包含系统范围内的内核模式模块和当前进程的用户模式模块。

 

可以通过目标的虚拟地址空间中的基址或由引擎为目标维护的模块列表中的索引来指定模块。 模块的索引等于其在模块列表中的位置，因此，如果卸载具有较低索引的模块，则此索引会发生更改。 所有已卸载的模块都有索引;它们始终高于已加载模块的索引。 只要模块的基址仍处于加载，模块的基址就不会更改;在某些情况下，如果卸载并重新加载模块，则可能会更改。

索引为介于零和目标中的模块数减1之间的数字。 可以通过调用[**GetNumberModules**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getnumbermodules)找到当前进程中的模块数。

索引可用于通过调用[**GetModuleByIndex**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmodulebyindex)查找基址。 可以使用[**GetSymbolModule**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolmodule)查找拥有具有给定名称的符号的模块的基址。

以下方法返回指定模块的索引和基址：

-   若要查找具有给定模块名称的模块，请使用[**GetModuleByModuleName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmodulebymodulename)。

-   [**GetModuleByOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmodulebyoffset)返回其虚拟地址范围包含给定地址的模块。 此方法可用于在给定模块基址的情况下查找模块索引。

以下方法返回通过基址或索引指定的模块的相关信息：

-   模块的名称由[**GetModuleNames**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmodulenames)和[**GetModuleNameString**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmodulenamestring)返回。

-   [**GetModuleVersionInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmoduleversioninformation)返回模块的版本信息。

-   用于描述模块的某些参数由[**GetModuleParameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getmoduleparameters)返回。 有关此方法返回的参数的详细信息，请参阅[**DEBUG\_MODULE\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_module_parameters)。

### <a name="span-idunloaded_modulesspanspan-idunloaded_modulesspanunloaded-modules"></a><span id="unloaded_modules"></span><span id="UNLOADED_MODULES"></span>卸载的模块

在用户模式调试过程中，仅在 Windows Server 2003 和更高版本的 Windows 中跟踪卸载的模块。 Windows 的早期版本仅在内核模式下跟踪卸载的模块。 跟踪这些标记后，它们会在加载的模块之后进行索引。 因此，任何搜索目标模块的方法都将搜索所有已加载的模块，然后搜索已卸载的模块。 卸载的模块可用于分析尝试调用已卸载代码时导致的失败。

### <a name="span-idsynthetic_modulesspanspan-idsynthetic_modulesspan-synthetic-modules"></a><span id="synthetic_modules"></span><span id="SYNTHETIC_MODULES"></span>综合模块

可以通过创建*合成模块*来标记内存区域。 这些模块不能包含实符号，但是它们可以包含合成符号。 方法[**AddSyntheticModule**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-addsyntheticmodule)创建新的合成模块。 可以使用[**RemoveSyntheticModule**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-removesyntheticmodule)删除综合模块。 重新加载目标中的所有模块将删除所有综合模块。

### <a name="span-idimage_pathspanspan-idimage_pathspanimage-path"></a><span id="image_path"></span><span id="IMAGE_PATH"></span>映像路径

搜索可执行映像时，引擎将使用该*可执行图像路径*。

可执行映像路径可以包含由分号（ **;** ）分隔的多个目录。 将按顺序搜索这些目录。

有关可执行映像路径的概述，请参阅可执行映像路径。

若要将目录添加到可执行映像路径，请使用方法[**AppendImagePath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-appendimagepath)。 整个可执行图像路径由[**GetImagePath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getimagepath)返回，可使用[**SetImagePath**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-setimagepath)进行更改。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关进程和虚拟进程的详细信息，请参阅[线程和进程](controlling-threads-and-processes.md)。

 

 





