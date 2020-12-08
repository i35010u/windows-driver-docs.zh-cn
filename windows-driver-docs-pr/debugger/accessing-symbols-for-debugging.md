---
title: 访问调试符号
description: 访问调试符号
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e65ee7c3eeccef7e02e69a8e53c9a8e041c4e6c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824357"
---
# <a name="accessing-symbols-for-debugging"></a>访问调试符号


## <span id="ddk_debugging_user_mode_processes_without_symbols_dbg"></span><span id="DDK_DEBUGGING_USER_MODE_PROCESSES_WITHOUT_SYMBOLS_DBG"></span>


正确设置用于调试的符号可能是一种具有挑战性的任务，尤其是对于内核调试。 它通常要求您知道您的计算机上所有产品的名称和版本。 调试器必须能够找到与产品发行版和 service pack 对应的每个符号文件。

这可能会导致包含长目录列表的超长符号路径。

若要在协调符号文件时简化这些问题，可将符号文件收集到 *符号存储区* 中，然后由 *符号服务器* 访问。

符号存储区是符号文件、索引和工具的集合，可供管理员用来添加和删除文件。 根据时间戳和图像大小等唯一参数对文件进行索引。 符号存储还可以包含可执行的图像文件，这些文件可使用符号服务器提取。 适用于 Windows 的调试工具包含一个名为 [SymStore](symstore.md)的符号存储创建工具。

符号服务器使调试器能够自动从符号存储区中检索正确的符号文件，而用户无需知道产品名称、版本或生成号。 适用于 Windows 的调试工具包含一个名为 [SymSrv](symsrv.md)的符号服务器。 通过在符号路径中包含某个文本字符串来激活符号服务器。 每当调试器需要为新加载的模块加载符号时，它都会调用符号服务器来查找相应的符号文件。

如果希望使用不同于 SymSrv 提供的符号搜索方法，可以创建自己的符号服务器 DLL。 有关实现此类符号服务器的详细信息，请参阅 [其他符号](other-symbol-servers.md)服务器。

如果要执行用户模式调试，将需要目标应用程序的符号。 如果正在执行内核模式调试，则需要为要调试的驱动程序以及 Windows 公共符号提供符号。 Microsoft 已使用 Microsoft 产品的公共符号创建了一个符号存储区;此符号存储在 internet 上可用。 可以使用 [**. symfix (设置符号存储路径)**](-symfix--set-symbol-store-path-.md) 命令加载这些符号，前提是你在调试器运行时有权访问 internet。 有关详细信息或者要确定如何手动安装这些符号，请参阅 [安装 Windows 符号文件](installing-windows-symbol-files.md)。

本节包括：

[安装 Windows 符号文件](installing-windows-symbol-files.md)

[符号存储和符号服务器](symbol-stores-and-symbol-servers.md)

[延迟符号加载](deferred-symbol-loading.md)

 

 





