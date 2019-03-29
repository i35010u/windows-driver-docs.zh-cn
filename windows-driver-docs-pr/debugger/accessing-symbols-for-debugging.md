---
title: 访问调试符号
description: 访问调试符号
ms.assetid: a0f52dc3-6903-4d63-b74c-5c16960a7cb6
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 671035d7aa60d6e715552c2cc26b5274e1203f96
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564336"
---
# <a name="accessing-symbols-for-debugging"></a>访问调试符号


## <span id="ddk_debugging_user_mode_processes_without_symbols_dbg"></span><span id="DDK_DEBUGGING_USER_MODE_PROCESSES_WITHOUT_SYMBOLS_DBG"></span>


设置正确的调试符号可以是具有挑战性的任务，尤其是对于内核调试。 它通常要求你知道的名称和版本的所有产品在计算机上。 调试器必须能够找到每个对应于产品版本和 service pack 的符号文件。

这可能导致在相当长的符号路径中包含的一长串的目录。

若要简化这些问题相协调的符号文件，符号文件可以收集到*符号存储区*，然后通过访问哪一*符号服务器*。

符号存储区是符号文件、 索引和工具，可以由管理员用来添加和删除文件的集合。 这些文件编制索引根据唯一参数，例如时间戳和图像大小。 符号存储区还可以包含可以使用符号服务器提取这些可执行文件的图像文件。 调试工具的 Windows 包含名为的符号存储区创建工具[SymStore](symstore.md)。

符号服务器还允许调试器可以自动从符号检索正确的符号文件存储，而用户无需知道产品名称，不释放，或生成号。 调试工具的 Windows 包含名为的符号服务器[SymSrv](symsrv.md)。 符号服务器激活的符号路径中包括的特定文本字符串。 每次调试器需要加载符号的新加载的模块，它调用符号服务器查找适当的符号文件。

如果想要使用不同的方法符号搜索所提供的 SymSrv 相比，可以创建自己的符号服务器 DLL。 有关实现符号服务器的详细信息，请参阅[符号的其他服务器](other-symbol-servers.md)。

如果您正在执行用户模式下调试，则需要符号为目标应用程序。 如果您正在执行内核模式调试，则需要进行调试，该驱动程序的符号，以及 Windows 公共符号。 Microsoft 已与 Microsoft 产品; 公共符号创建符号存储区此符号存储区是在 internet 上可用。 可以使用加载这些符号[ **.symfix （设置符号存储区路径）** ](-symfix--set-symbol-store-path-.md)命令时，只要您的调试器运行时有权访问 internet。 有关详细信息，或以确定如何手动安装这些符号，请参阅[安装 Windows 符号文件](installing-windows-symbol-files.md)。

本部分包括：

[安装 Windows 符号文件](installing-windows-symbol-files.md)

[符号存储区和符号服务器](symbol-stores-and-symbol-servers.md)

[延迟加载的符号](deferred-symbol-loading.md)

 

 





