---
title: 模块
description: 模块
ms.assetid: 0cd99869-4014-4f9f-b5f1-d06c69fd134e
keywords:
- 模块的符号
- 模块
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 07765e1cba145cd40b1ff2ec39c3fe303ec27d59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361502"
---
# <a name="modules"></a>模块


## <span id="modules"></span><span id="MODULES"></span>


*图像*是可执行文件、 DLL 或 Windows 用户模式进程或内核的一部分已加载的驱动程序。 从其加载图像的文件称为其*映像文件*。

[调试器引擎](introduction.md#debugger-engine)缓存一系列*模块*每个进程 （或在内核模式下，虚拟过程）。 通常，此列表中的每个模块表示进程中的图像。 可与目标使用同步引擎的模块列表**重新加载**。

**请注意**  在内核模式调试中，虚拟进程的引擎的模块列表包含整个系统的内核模式模块和当前进程的用户模式模块。

 

可以通过在目标的虚拟地址空间中，其基址指定模块或通过在模块列表中的索引引擎维护为目标。 模块的索引等于列表中的模块，其位置并因此会更改此索引，如果具有较低索引的模块被卸载。 所有已卸载的模块具有索引;这些是始终高于已加载的模块的索引。 只要保持加载; 不会更改模块的基址在某些情况下它可能会更改如果卸载，然后重新加载该模块。

索引是 0 到减一目标中的模块数之间的数字。 可以通过调用找到的当前进程中的模块数[ **GetNumberModules**](https://msdn.microsoft.com/library/windows/hardware/ff547927)。

索引可用于通过调用找到的基址[ **GetModuleByIndex**](https://msdn.microsoft.com/library/windows/hardware/ff547080)。 使用可以找到拥有具有给定名称的符号的模块的基址[ **GetSymbolModule**](https://msdn.microsoft.com/library/windows/hardware/ff549112)。

以下方法返回的索引和基址指定的模块：

-   若要查找给定的模块名称的模块，请使用[ **GetModuleByModuleName**](https://msdn.microsoft.com/library/windows/hardware/ff547095)。

-   返回其虚拟地址范围包含给定的地址模块[ **GetModuleByOffset**](https://msdn.microsoft.com/library/windows/hardware/ff547132)。 此方法可用于查找给定模块的基址的模块索引。

以下方法返回有关按基地址或索引指定的模块的信息：

-   返回模块的名称[ **GetModuleNames** ](https://msdn.microsoft.com/library/windows/hardware/ff547146)并[ **GetModuleNameString**](https://msdn.microsoft.com/library/windows/hardware/ff547149)。

-   返回模块的版本信息[ **GetModuleVersionInformation**](https://msdn.microsoft.com/library/windows/hardware/ff547170)。

-   一些用于描述模块的参数返回的[ **GetModuleParameters**](https://msdn.microsoft.com/library/windows/hardware/ff547161)。 此方法返回的参数的详细信息，请参阅[**调试\_模块\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff541514)。

### <a name="span-idunloadedmodulesspanspan-idunloadedmodulesspanunloaded-modules"></a><span id="unloaded_modules"></span><span id="UNLOADED_MODULES"></span>卸载的模块

在用户模式调试，仅在 Windows Server 2003 和更高版本的 Windows 中跟踪已卸载的模块。 早期版本的 Windows 仅跟踪在内核模式下卸载的模块。 它们跟踪时，它们编制索引后已加载的模块。 因此搜索目标的模块的任何方法将搜索所有已加载的模块，然后卸载的模块。 卸载的模块可用于分析导致尝试调用卸载的代码的失败。

### <a name="span-idsyntheticmodulesspanspan-idsyntheticmodulesspan-synthetic-modules"></a><span id="synthetic_modules"></span><span id="SYNTHETIC_MODULES"></span> 综合模块

*综合模块*可以作为一种方式标记的内存区域中创建。 这些模块不能包含实际的符号，但它们可以包含综合符号。 该方法[ **AddSyntheticModule** ](https://msdn.microsoft.com/library/windows/hardware/ff537937)创建一个新的综合模块。 可以使用删除综合模块[ **RemoveSyntheticModule**](https://msdn.microsoft.com/library/windows/hardware/ff554536)。 重新加载在目标中的所有模块中删除所有综合模块。

### <a name="span-idimagepathspanspan-idimagepathspanimage-path"></a><span id="image_path"></span><span id="IMAGE_PATH"></span>映像路径

*可执行映像路径*搜索可执行映像时，引擎使用。

可执行映像路径可以包含的以分号分隔的多个目录 (**;**)。 按顺序将搜索这些目录。

有关可执行映像路径的概述，请参阅可执行文件映像路径。

若要将目录添加到可执行映像路径，使用方法[ **AppendImagePath**](https://msdn.microsoft.com/library/windows/hardware/ff538092)。 返回整个可执行映像路径[ **GetImagePath** ](https://msdn.microsoft.com/library/windows/hardware/ff546851) ，可以使用更改[ **SetImagePath**](https://msdn.microsoft.com/library/windows/hardware/ff556708)。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关进程和虚拟进程的详细信息，请参阅[线程和进程](controlling-threads-and-processes.md)。

 

 





