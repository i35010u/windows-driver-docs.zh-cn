---
title: 延迟符号加载
description: 延迟符号加载
ms.assetid: 58771089-dd0c-4ea9-8a9a-41553f290e88
keywords:
- 延迟的符号加载
- 符号，延迟加载的符号
- 延迟的符号加载
- 符号，延迟加载的符号
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 853eba6fce8395fb81e6a37e8e33bfefed0ba557
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346313"
---
# <a name="deferred-symbol-loading"></a>延迟符号加载


## <span id="ddk_deferred_symbol_loading_dbg"></span><span id="DDK_DEFERRED_SYMBOL_LOADING_DBG"></span>


默认情况下，符号信息是不实际加载目标模块加载时。 相反，符号进行加载由调试器需要它们。 这称为*延迟的符号加载*或*延迟符号加载*。 启用此选项后，调试器在遇到无法识别的符号时加载符号。

如果更改符号路径，例如通过使用[ **.sympath （设置符号路径）** ](-sympath--set-symbol-path-.md)命令、 所有已加载模块导出的符号与延迟重新加载。 使用完整的 PDB 符号的模块的符号将延迟重新加载新的路径不能再包含用于加载 PDB 符号的原始路径。 如果新路径仍包含 PDB 符号文件的原始路径，这些符号将不会延迟重新加载。

当禁用延迟加载的符号时，进程启动可以要慢得多，因为每当模块读取所有符号加载。

在 WinDbg 中，延迟的符号加载行为可以修改的情况下使用具有任何模块的前缀符号[解析非限定符号](debug---resolve-unqualified-symbols.md)选项卡上**调试**菜单。

可以通过使用延迟的符号加载重写[ **ld （加载符号）** ](ld--load-symbols-.md)命令或[ **.reload （重新加载模块）** ](-reload--reload-module-.md)命令 **/f**选项。 这些都强制要求要立即加载的指定的符号尽管延迟加载的其他符号。

默认情况下，启用延迟的符号加载。 在 CDB 和 KD， **-s** [命令行选项](command-line-options.md)将关闭此选项。 它可以也关闭 CDB 中通过使用*LazyLoad*变量中[tools.ini](configuring-tools-ini.md)文件。 调试器开始运行后，此选项可以打开或关闭通过使用[ **.symopt + 0x4** ](-symopt--set-symbol-options-.md)或 **.symopt 0x4**分别。

 

 





