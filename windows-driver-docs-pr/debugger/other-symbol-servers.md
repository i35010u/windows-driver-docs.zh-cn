---
title: 其他符号服务器
description: 其他符号服务器
ms.assetid: 69d88a60-88b6-4118-9f8b-0d7b80bad1ab
keywords:
- 符号服务器，编写你自己的符号服务器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: d87721e74cbf37f9aa17eacca34ebd2db30be2f0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330951"
---
# <a name="other-symbol-servers"></a>其他符号服务器


## <span id="ddk_using_other_symbol_servers_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_SERVERS_DBG"></span>


如果想要为你的符号搜索使用不同的方法，可以提供您自己的符号服务器 DLL 而不是使用 SymSrv。

### <a name="span-idsettingthesymbolpathspanspan-idsettingthesymbolpathspansetting-the-symbol-path"></a><span id="setting_the_symbol_path"></span><span id="SETTING_THE_SYMBOL_PATH"></span>设置符号路径

在实现 SymSrv 以外的符号服务器时，调试器的符号路径设置的相同方式与使用 SymSrv。 请参阅[SymSrv](symsrv.md)有关符号路径语法的说明。 你需要进行的唯一更改是替换的字符串**symsrv.dll**你自己的符号服务器 DLL 的名称。

如果您愿意，你可以随意使用的参数内不同的语法来表示不同的技术，如 UNC 路径、 数据库的 SQL 标识符或 Internet 规范。

### <a name="span-idimplementingyourownsymbolserverspanspan-idimplementingyourownsymbolserverspanimplementing-your-own-symbol-server"></a><span id="implementing_your_own_symbol_server"></span><span id="IMPLEMENTING_YOUR_OWN_SYMBOL_SERVER"></span>实现符号服务器

在服务器的核心部分是与 DbgHelp 到查找符号进行通信的代码。 每次 DbgHelp 需要新加载的模块的符号，它调用符号服务器查找适当的符号文件。 符号服务器查找唯一的参数，例如时间戳或图像大小根据每个文件。 服务器返回所请求的文件已验证的路径。 若要实现这个目的，服务器必须导出**SymbolServer**函数。

服务器还应支持**SymbolServerSetOptions**并**SymbolServerGetOptions**函数。 并将调用 DbgHelp **SymbolServerClose**函数，如果它由服务器导出的。 请参阅[符号服务器 API](symbol-server-api.md)有关记录这些例程了。

不得更改返回的符号服务器的实际符号文件名称。 DbgHelp 在多个位置中存储的符号文件的名称。 因此，服务器必须返回相同名称的文件，作为该指定符号已请求时。 此限制才可确保在符号加载过程中显示的符号名称是编程人员将识别的。

### <a name="span-idrestrictionsonmultiplesymbolserversspanspan-idrestrictionsonmultiplesymbolserversspanrestrictions-on-multiple-symbol-servers"></a><span id="restrictions_on_multiple_symbol_servers"></span><span id="RESTRICTIONS_ON_MULTIPLE_SYMBOL_SERVERS"></span>多个符号服务器上的限制

DbgHelp 支持一次只有一个符号服务器的使用。 符号路径可以包含多个实例的相同的符号服务器 DLL，但不是能两个不同的符号服务器 Dll。 这不是很多限制，因为你仍可自由地在你的符号路径，每个都指向不同的符号存储区中包括的符号服务器的多个实例。 但如果你想要切换这两个不同的符号服务器 Dll，您将必须每次更改符号路径。

### <a name="span-idinstallingyoursymbolserverspanspan-idinstallingyoursymbolserverspaninstalling-your-symbol-server"></a><span id="installing_your_symbol_server"></span><span id="INSTALLING_YOUR_SYMBOL_SERVER"></span>安装符号服务器

符号服务器安装的详细信息将取决于你的情况。 你可能想要设置复制符号服务器 DLL 的安装过程，并设置\_NT\_符号\_PATH 环境变量自动。

具体取决于你的服务器中使用的技术，您可能还需要安装或访问的符号数据本身。

 

 





