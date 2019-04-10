---
title: Microsoft 公共符号服务器
description: Microsoft 符号服务器使 Windows 调试器符号公开可用。
ms.assetid: b0d38104-c386-4d20-8d9c-7701347c1643
keywords:
- SymSrv，公共 Microsoft 符号
- 符号服务器，公共 Microsoft 符号
- 公共符号存储区
- Microsoft 符号存储区
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: f53f44ee1628fddd1bdd00c05b5ca05642af32a0
ms.sourcegitcommit: 58d5457779071709faab68e44decc3c48a2cf975
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2019
ms.locfileid: "59362914"
---
# <a name="microsoft-public-symbol-server"></a>Microsoft 公共符号服务器


**服务器状态：** 没有已知的问题： white_check_mark: <br> Microsoft 公共符号服务器是完全正常运行。 <br>
请将错误报告到的任何已知的问题[ windbgfb@microsoft.com ](mailto:windbgfb@microsoft.com)。 

---

Microsoft 符号服务器使 Windows 调试器符号公开可用。

您可以按以下方式来引用符号路径中直接向公共符号服务器：

```console
set _NT_SYMBOL_PATH=srv*DownstreamStore*https://msdl.microsoft.com/download/symbols
```

*DownstreamStore*必须在本地计算机或将用于将符号缓存的网络上指定一个目录。 此下游存储包含符号的调试器已访问;永远不会被访问的符号的优点在于绝大多数会保留在 microsoft 符号存储区。 这使你的下游存储相对较小，并允许符号服务器，若要快速开始工作，仅一次下载每个文件。

若要避免在键入此长符号路径，请使用[ **.symfix （设置符号存储区路径）** ](-symfix--set-symbol-store-path-.md)命令。 以下命令将公共符号存储区追加到现有的符号路径：

```dbgcmd
.symfix+ C:\MySymbols
```

如果省略本地符号缓存位置，则将使用调试器安装目录的符号子目录。

使用[ **.sympath （设置符号存储区路径）** ](-symfix--set-symbol-store-path-.md)命令以显示完整的符号路径。 此示例演示如何使用 symfix 创建本地符号缓存并使用 Microsoft http 符号服务器。

```dbgcmd
0: kd> .symfix c:\MyCache
0: kd> .sympath
Symbol search path is: srv*
Expanded Symbol search path is: cache*c:\MyCache;SRV*https://msdl.microsoft.com/download/symbols
```

有关处理符号的详细信息，请参阅[Windows 调试器的符号路径](https://docs.microsoft.com/windows-hardware/drivers/debugger/symbol-path)。

**符号文件压缩**

Microsoft 符号服务器提供符号文件的压缩的版本。 这些文件具有的文件名扩展，以指示其进行压缩的结尾处的下划线。 例如，ntdll.dll 的 PDB 现在以 ntdll.pd\_。 当 SymProxy 下载压缩的文件时，它将存储在本地文件系统中解压缩该文件。 可以设置 DontUncompress 注册表项以 SymProxy 中禁用此行为。

请参阅调试器主题[SymStore](symstore.md)有关使用 SymStore.exe /compress 存储符号在符号服务器上压缩的信息。

 

 





