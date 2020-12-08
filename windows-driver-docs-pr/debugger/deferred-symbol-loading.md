---
title: 延迟符号加载
description: 延迟符号加载
keywords:
- 延迟的符号加载
- 符号，延迟符号加载
- 延迟符号加载
- 符号，延迟符号加载
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ef484fa1945a13eda1f3787f8f457e02ce70f22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794025"
---
# <a name="deferred-symbol-loading"></a>延迟符号加载


## <span id="ddk_deferred_symbol_loading_dbg"></span><span id="DDK_DEFERRED_SYMBOL_LOADING_DBG"></span>


默认情况下，加载目标模块时，不会实际加载符号信息。 而是在需要时由调试器加载符号。 这称为 *延迟符号加载* 或 *延迟符号加载*。 启用此选项后，调试器将在遇到无法识别的符号时加载符号。

当符号路径发生更改时（例如，通过使用 [**. sympath (设置符号路径)**](-sympath--set-symbol-path-.md) 命令），包含导出符号的所有已加载模块都将延迟重新加载。 如果新路径不再包含用于加载 PDB 符号的原始路径，则将会惰式重载包含完整 PDB 符号的模块的符号。 如果新路径仍包含 PDB 符号文件的原始路径，则不会惰式重载这些符号。

如果禁用延迟的符号加载，则进程启动速度会慢得多，因为每次加载模块时都读取所有符号。

在 WinDbg 中，可以通过使用 "**调试**" 菜单上的 "[解析非限定符号](debug---resolve-unqualified-symbols.md)" 选项，为没有模块前缀的符号修改延迟的符号加载行为。

您可以使用 [**ld (负载符号)**](ld--load-symbols-.md)命令或使用 **/f** 选项重载 [**(重载模块)**](-reload--reload-module-.md)命令重写延迟的符号加载。 这会强制立即加载指定的符号，但会延迟加载其他符号。

默认情况下，将启用延迟的符号加载。 在 CDB 和 KD 中， **-s** [命令行选项](command-line-options.md) 将关闭此选项。 还可以通过使用 [tools.ini](configuring-tools-ini.md)文件中的 *LAZYLOAD* 变量在 CDB 中关闭它。 调试器运行后，可以使用 [**. symopt + 0x4**](-symopt--set-symbol-options-.md) 或 **. symopt-0x4** 来打开或关闭此选项。

 

 





