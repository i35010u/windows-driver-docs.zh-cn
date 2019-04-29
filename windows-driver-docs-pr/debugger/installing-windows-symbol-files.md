---
title: 安装 Windows 符号文件
description: 安装 Windows 符号文件
ms.assetid: fbafb14c-9b92-47c5-9954-5c5ba2301c47
keywords:
- 符号 Windows
- 符号、 用户模式
ms.date: 03/26/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2a2ec8db9b2230f4b5a2d62c0780bed6522c0f4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371657"
---
# <a name="installing-windows-symbol-files"></a>安装 Windows 符号文件

调试 Windows 内核，驱动程序或应用程序之前，需要能够访问正确的符号文件。 获取 Windows 符号的官方方法是使用 Microsoft 符号服务器。 符号服务器根据需要为调试工具提供符号。 从符号服务器下载符号文件后，该文件将缓存在本地计算机上，以供快速访问。 

可以连接到 Microsoft 符号服务器使用的一种简单的用法[ **.symfix （设置符号存储区路径）** ](-symfix--set-symbol-store-path-.md)命令。 有关完整详细信息，请参阅[Microsoft 公共符号](microsoft-public-symbols.md)。

> [!IMPORTANT]
> 我们不能再为 Windows 发布脱机符号包。 更快的 Windows 更新的频率表示的 Windows 调试符号快速进行过期。 我们已显著改进的联机[Microsoft 符号服务器](microsoft-public-symbols.md)提供所有 Windows 版本和更新的符号的。 您可以找到更多有关这在此[博客文章](https://blogs.msdn.microsoft.com/windbg/2017/10/18/update-on-microsofts-symbol-server/)。 
>
> 有关如何为未连接到 Internet 的计算机检索符号的信息，请参阅[通过 SymChk 使用清单文件](using-a-manifest-file-with-symchk.md)。

如果要调试的用户模式应用程序，您需要安装此的应用程序的符号。

如果您有其符号，但不是 Windows 符号，则可以调试应用。 但是，则结果将为更多的限制。 您将仍能够单步执行应用代码中，但这需要 （如获得堆栈跟踪） 内核进行分析的任何调试器活动很可能会失败。
