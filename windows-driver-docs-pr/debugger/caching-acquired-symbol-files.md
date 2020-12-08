---
title: 缓存获取的符号文件
description: 缓存获取的符号文件
keywords:
- SymProxy，缓存
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bb432e33306da8544d0994c346a53cb2e2fabe4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828261"
---
# <a name="caching-acquired-symbol-files"></a>缓存获取的符号文件


通常情况下，SymProxy 会将它获取的文件缓存到 Internet Information Services (IIS) 中指定的目录中，作为关联网站的虚拟根目录。 然后 IIS 使该文件可供客户端调试器使用。 由于调试器无法直接从 HTTP 打开文件，因此它会将文件复制到由符号路径指定的本地缓存：

```text
srv*c:\localcache*https://server/symbols
```

在此示例中，客户端调试器将文件复制到 c： \\ localcache。 在这种情况下，该文件将被 SymProxy 复制到网站的虚拟根目录一次，并再次复制到其本地缓存。

可以避免第二次复制操作并加快处理速度。 若要执行此操作，必须首先将网站的虚拟根共享为可由调试器访问的 UNC 路径。 例如，此路径称为 \\ \\ 服务器 \\ 符号。 然后，必须删除 MIME 类型的 IIS 配置：

**删除 MIME 类型的 IIS 配置**

1.  从 " **管理工具** " **Internet Information Services (IIS) 管理器** 打开。

2.  展开 **"网站"**。

3.  右键单击 " **默认** 网站"。

4.  右键单击 **符号** 虚拟目录，然后选择 " **属性**"。

5.  单击 " **HTTP 标头** " 选项卡。

6.  单击 " **MIME 类型** "。

7.  在标记为 " **已注册 MIME 类型**" 的列表框中选择所有类型。

8.  单击 " **删除** "。

9.  若要退出 **MIME 类型** 对话框，请单击 **"确定"**。

10. 若要退出 **符号属性**，请单击 **"确定"**。

这将导致 IIS 为网站上的所有事务返回 **未找到** 调试客户端的文件。 但是，它不会阻止 SymProxy 用文件填充虚拟根目录。

删除适用于 MIME 类型的 IIS 配置后，请将调试器客户端配置为先在 HTTP 存储和映射到存储的虚拟根目录的共享中查找符号，如下所示：

```text
srv**https://server/symbols;srv*\\server\symbols
```

在前面的示例中，符号路径 (srv 的第一个元素是 \* \* https://server/symbols) 从 HTTP 存储获取文件，并将它们作为本地缓存复制到默认符号存储区中。 指定的缓存没有任何重要性，因为从未从 HTTP 存储区接收到任何文件。 此失败后，它会尝试从存储的虚拟根目录的实际位置获取文件 (srv \* \\ \\ 服务器 \\ 符号) 。 此尝试将成功，因为文件将作为之前路径处理的副作用复制到该位置。

 

 





