---
title: Microsoft 公共符号服务器
description: Microsoft 符号服务器使 Windows 调试器符号公开可用。
ms.assetid: b0d38104-c386-4d20-8d9c-7701347c1643
keywords:
- SymSrv, 公有 Microsoft 符号
- 符号服务器, 公共 Microsoft 符号
- 公共符号存储区
- Microsoft 符号存储区
ms.date: 04/26/2018
ms.localizationpriority: medium
ms.openlocfilehash: 621cfe78438051ad08856e70dca1ec1f9e2a3cb1
ms.sourcegitcommit: d5adc4f20ecdf94d3940eb09427b29774e9c1e78
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2019
ms.locfileid: "71344627"
---
# <a name="microsoft-public-symbol-server"></a>Microsoft 公共符号服务器


**服务器状态:** MSDL 服务中断 <br> 
 我们收到了某些区域中有关存储问题的报告。 客户可能无法解析公共符号。 团队正在积极调查并处理解决方法。 <br>
请向[windbgfb@microsoft.com](mailto:windbgfb@microsoft.com)报告任何已知问题。 

---

Microsoft 符号服务器使 Windows 调试器符号公开可用。

可以通过以下方式直接在符号路径中引用公共符号服务器:

```console
set _NT_SYMBOL_PATH=srv*DownstreamStore*https://msdl.microsoft.com/download/symbols
```

*DownstreamStore*必须指定将用于缓存符号的本地计算机或网络上的目录。 此下游存储包含调试器已访问的符号;大多数从未访问过的符号将保留在 Microsoft 的符号存储区中。 这会使下游存储相对较小, 并允许符号服务器快速工作, 仅下载每个文件一次。

若要避免键入此长符号路径, 请使用[ **. symfix (Set 符号存储区路径)** ](-symfix--set-symbol-store-path-.md)命令。 以下命令将公共符号存储区追加到现有符号路径:

```dbgcmd
.symfix+ C:\MySymbols
```

如果省略了本地符号缓存位置, 将使用调试器安装目录的符号子目录。

使用 " [**sympath (Set 符号存储路径)** ](-symfix--set-symbol-store-path-.md) " 命令可显示完整的符号路径。 此示例演示如何使用 symfix 创建本地符号缓存并使用 Microsoft http 符号服务器。

```dbgcmd
0: kd> .symfix c:\MyCache
0: kd> .sympath
Symbol search path is: srv*
Expanded Symbol search path is: cache*c:\MyCache;SRV*https://msdl.microsoft.com/download/symbols
```

有关使用符号的详细信息, 请参阅[Windows 调试器的符号路径](https://docs.microsoft.com/windows-hardware/drivers/debugger/symbol-path)。

**符号文件压缩**

Microsoft 符号服务器提供了符号文件的压缩版本。 文件扩展名的末尾有一个下划线, 用于指示已对其进行压缩。 例如, ntdll.dll 的 PDB 可用作 ntdll.dll\_。 当 SymProxy 下载压缩文件时, 它会将文件解压缩到本地文件系统中。 DontUncompress 注册表项可设置为在 SymProxy 中禁用此行为。

有关使用 SymStore/compress 存储在符号服务器上压缩的符号的信息, 请参阅调试器主题[SymStore](symstore.md) 。

 

 





