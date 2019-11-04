---
title: Microsoft 公共符号服务器
description: Microsoft 符号服务器使 Windows 调试程序符号公开可用。
ms.assetid: b0d38104-c386-4d20-8d9c-7701347c1643
keywords:
- SymSrv, 公共的 Microsoft 符号
- 符号服务器, 公共的 Microsoft 符号
- 公共符号存储
- Microsoft 符号存储
ms.date: 04/26/2018
ms.localizationpriority: High
ms.openlocfilehash: bc3e794ba35bb3cef1a8db136a9bea2ce0eaef35
ms.sourcegitcommit: fe0b8b8b162c6fc0afd82dd03e83d41be0bc5d12
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2019
ms.locfileid: "72980746"
---
# <a name="microsoft-public-symbol-server"></a>Microsoft 公共符号服务器


**服务器状态：** MSDL 服务中断 <br> 我们在所有区域收到了错误报告。 客户可能无法解析公共符号。 团队正在积极调查此问题并努力提供解决方法。  <br>
请将任何已知问题报告给 [windbgfb@microsoft.com](mailto:windbgfb@microsoft.com)。 

---

Microsoft 符号服务器使 Windows 调试程序符号公开可用。

可通过以下方式直接引用符号路径中的公共符号服务器：

```console
set _NT_SYMBOL_PATH=srv*DownstreamStore*https://msdl.microsoft.com/download/symbols
```

*DownstreamStore* 必须在本地计算机或网络上指定一个将要用于缓存符号的目录。 此下游存储保存调试程序已访问的符号；大多数从未访问过的符号保留在 Microsoft 的符号存储中。 这样可以让下游存储保持相对较小的大小，使符号服务器可以快速运行，仅下载每个文件一次。

为了避免键入这个长的符号路径，请使用 [ **.symfix（设置符号存储路径）** ](-symfix--set-symbol-store-path-.md)命令。 以下命令将公共符号存储追加到现有的符号路径：

```dbgcmd
.symfix+ C:\MySymbols
```

如果省略本地符号缓存位置，则会使用调试程序安装目录的 sym 子目录。

请使用 [ **.sympath（设置符号存储路径）** ](-symfix--set-symbol-store-path-.md)命令显示完整的符号路径。 以下示例显示了如何使用 symfix 来创建本地符号缓存，以及如何使用 Microsoft http 符号服务器。

```dbgcmd
0: kd> .symfix c:\MyCache
0: kd> .sympath
Symbol search path is: srv*
Expanded Symbol search path is: cache*c:\MyCache;SRV*https://msdl.microsoft.com/download/symbols
```

若要详细了解如何处理符号，请参阅 [Windows 调试程序的符号路径](https://docs.microsoft.com/windows-hardware/drivers/debugger/symbol-path)。

**符号文件压缩**

Microsoft 符号服务器提供压缩版符号文件。 这些文件在文件扩展名的末尾有一条下划线，表示它们是压缩的。 例如，ntdll.dll 的 PDB 以 ntdll.pd\_ 形式提供。 SymProxy 在下载压缩文件时，会将其存储在本地文件系统中。 可以通过设置 DontUncompress 注册表项在 SymProxy 中禁用此行为。

请参阅调试程序主题 [SymStore](symstore.md)，了解如何使用 SymStore.exe /compress 在符号服务器上存储自己的已压缩符号。

 

 





