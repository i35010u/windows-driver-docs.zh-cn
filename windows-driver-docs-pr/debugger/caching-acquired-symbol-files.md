---
title: 缓存获取的符号文件
description: 缓存获取的符号文件
ms.assetid: 2aedc67f-27f3-46f4-8369-504e525b8c18
keywords:
- SymProxy，缓存
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0bb8e5fcef9b42bf4f1d2fa136118c3e43173d49
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569177"
---
# <a name="caching-acquired-symbol-files"></a>缓存获取的符号文件


通常情况下，SymProxy 缓存它将获取指定 Internet 信息服务 (IIS) 中为关联的 Web 站点的虚拟根目录的目录中的文件。 然后 IIS 使该文件可供客户端调试器。 因为调试器不能直接从 HTTP 打开文件，它会将文件复制到本地缓存中，指定的符号路径中：

```text
srv*c:\localcache*https://server/symbols
```

在此示例中，客户端调试器将文件复制到 c:\\localcache。 在这种情况下，调试程序对其本地缓存一次通过 SymProxy 虚拟根目录的网站，并再次两次-复制该文件。

就可以避免第二个复制操作并提高处理速度。 若要执行此操作，必须首先为调试程序可以访问的 UNC 路径共享的虚拟根目录的 Web 站点。 此路径名为示例中，出于\\ \\server\\符号。 然后必须删除 MIME 类型的 IIS 配置：

**若要删除的 MIME 类型的 IIS 配置**

1.  从**管理工具**打开**Internet Information Services (IIS) Manager**。

2.  展开**网站**。

3.  右键单击**默认网站**。

4.  右键单击**符号**虚拟目录，然后选择**属性**。

5.  单击**HTTP 标头**选项卡。

6.  单击**MIME 类型**。

7.  标记为列表框中选择所有类型**已注册的 MIME 类型**。

8.  单击**删除**。

9.  若要退出**MIME 类型**对话框中，单击**确定**。

10. 若要退出**符号属性**，单击**确定**。

这会导致 IIS 以返回**找不到文件**调试客户端，以便在网站上的所有事务。 但是，它不会阻止 SymProxy 与文件填充的虚拟根目录。

删除 MIME 类型的 IIS 配置后，配置调试器客户端，若要查找的符号的 HTTP 存储区中的第和共享映射到的虚拟根目录的具有该命令的存储区中：

```text
srv**https://server/symbols;srv*\\server\symbols
```

在前面的示例中，符号路径的第一个元素 (srv\* \* https://server/symbols)说要从 HTTP 存储区获取文件，并将它们复制到默认符号存储区作为本地缓存。 指定的缓存是不重要，因为没有文件收到过从 HTTP 存储区。 此次失败后，尝试获取它将文件从实际存储的虚拟根目录的位置 (srv\*\\\\server\\符号)。 此尝试成功，因为将文件复制到上一个路径处理的该位置产生了负面影响。

 

 





