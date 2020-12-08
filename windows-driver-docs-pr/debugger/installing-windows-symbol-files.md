---
title: 安装 Windows 符号文件
description: 安装 Windows 符号文件
keywords:
- 符号，Windows
- 符号，用户模式
ms.date: 03/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6d64ce4a99bce4765449b90d0255311635d55ec1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829729"
---
# <a name="installing-windows-symbol-files"></a>安装 Windows 符号文件

在调试 Windows 内核、驱动程序或应用程序之前，您需要访问相应的符号文件。 获取 Windows 符号的官方方法是使用 Microsoft 符号服务器。 符号服务器根据需要向调试工具提供符号。 从符号服务器下载符号文件后，它将缓存在本地计算机上，以便快速访问。 

你可以使用 [**. symfix (设置符号存储路径)**](-symfix--set-symbol-store-path-.md) 命令，连接到 Microsoft 符号服务器。 有关完整详细信息，请参阅 [Microsoft 公共符号](microsoft-public-symbols.md)。

> [!IMPORTANT]
> 我们不再发布 Windows 的脱机符号包。 Windows 更新节奏更快意味着 Windows 调试符号很快就会变得过时。 我们对联机 [Microsoft 符号服务器](microsoft-public-symbols.md) 进行了重大改进，其中所有 Windows 版本和更新的符号都可用。 可在此 [博客文章](/archive/blogs/windbg/update-on-microsofts-symbol-server)中找到有关此内容的详细信息。 
>
> 有关如何检索未连接到 Internet 的计算机的符号的信息，请参阅将 [清单文件与 SymChk 一起使用](using-a-manifest-file-with-symchk.md)。

如果打算调试用户模式应用，还需要安装此应用的符号。

如果你的应用程序的符号但不是 Windows 符号，则可以调试应用程序。 但是，结果会受到更多的限制。 你仍可以单步执行应用程序代码，但任何需要分析内核 (如获取堆栈跟踪) 的调试器活动都可能会失败。
