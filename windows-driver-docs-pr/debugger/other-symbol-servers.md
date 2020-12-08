---
title: 其他符号服务器
description: 其他符号服务器
keywords:
- 符号服务器，编写自己的符号服务器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f538b0a7e72595f0bc9a2491230af4d3d667978d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818635"
---
# <a name="other-symbol-servers"></a>其他符号服务器


## <span id="ddk_using_other_symbol_servers_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_SERVERS_DBG"></span>


如果希望将不同方法用于符号搜索，可以提供自己的符号服务器 DLL，而不是使用 SymSrv。

### <a name="span-idsetting_the_symbol_pathspanspan-idsetting_the_symbol_pathspansetting-the-symbol-path"></a><span id="setting_the_symbol_path"></span><span id="SETTING_THE_SYMBOL_PATH"></span>设置符号路径

实现除 SymSrv 以外的符号服务器时，将使用与 SymSrv 相同的方式设置调试器的符号路径。 有关符号路径语法的说明，请参阅 [SymSrv](symsrv.md) 。 你需要做的唯一更改是将字符串 **symsrv.dll** 替换为你自己的符号服务器 DLL 的名称。

如果需要，可以在参数中随意使用不同的语法，以指示使用不同的技术，如 UNC 路径、SQL 数据库标识符或 Internet 规范。

### <a name="span-idimplementing_your_own_symbol_serverspanspan-idimplementing_your_own_symbol_serverspanimplementing-your-own-symbol-server"></a><span id="implementing_your_own_symbol_server"></span><span id="IMPLEMENTING_YOUR_OWN_SYMBOL_SERVER"></span>实现自己的符号服务器

服务器的核心部分是与 Dbghelp.dll 通信以查找符号的代码。 每次 Dbghelp.dll 都需要新加载的模块的符号时，它会调用符号服务器来查找相应的符号文件。 符号服务器根据唯一参数（如时间戳或图像大小）查找每个文件。 服务器返回所请求文件的验证路径。 若要实现此功能，服务器必须导出 **SymbolServer** 函数。

服务器还应支持 **SymbolServerSetOptions** 和 **SymbolServerGetOptions** 函数。 如果服务器导出 Dbghelp.dll 函数，则该函数将调用 **SymbolServerClose** 函数。 有关这些例程的记录位置的信息，请参阅 [符号服务器 API](symbol-server-api.md) 。

不得更改符号服务器返回的实际符号文件名。 Dbghelp.dll 将符号文件的名称存储在多个位置。 因此，服务器必须返回与请求符号时指定的名称相同的文件。 若要确保在符号加载过程中显示的符号名称是程序员可识别的符号名称，则需要此限制。

### <a name="span-idrestrictions_on_multiple_symbol_serversspanspan-idrestrictions_on_multiple_symbol_serversspanrestrictions-on-multiple-symbol-servers"></a><span id="restrictions_on_multiple_symbol_servers"></span><span id="RESTRICTIONS_ON_MULTIPLE_SYMBOL_SERVERS"></span>对多个符号服务器的限制

Dbghelp.dll 支持一次只使用一个符号服务器。 符号路径可以包含相同符号服务器 DLL 的多个实例，但不能包含两个不同的符号服务器 Dll。 这并不是一种限制，因为你仍可以在符号路径中包含符号服务器的多个实例，每个实例指向不同的符号存储区。 但是，如果要在两个不同的符号服务器 Dll 之间切换，则每次都必须更改符号路径。

### <a name="span-idinstalling_your_symbol_serverspanspan-idinstalling_your_symbol_serverspaninstalling-your-symbol-server"></a><span id="installing_your_symbol_server"></span><span id="INSTALLING_YOUR_SYMBOL_SERVER"></span>安装符号服务器

你的符号服务器安装的详细信息将取决于你的情况。 你可能想要设置一个安装过程，该过程将复制符号服务器 DLL 并 \_ 自动设置 NT \_ 符号 \_ 路径环境变量。

根据服务器中使用的技术，你可能还需要安装或访问符号数据本身。

 

 





