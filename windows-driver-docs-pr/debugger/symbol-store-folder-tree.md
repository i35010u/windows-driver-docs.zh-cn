---
title: 符号存储文件夹树
description: 支持 SMB 和 HTTP 请求的符号存储是位于本地磁盘上的文件夹树。
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6adbca926a716bcf0d8b3a74292abe3f4441dc22
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806495"
---
# <a name="symbol-store-folder-tree"></a>符号存储文件夹树


支持 SMB 和 HTTP 请求的符号存储是位于本地磁盘上的文件夹树。

为了使管理保持简单，子文件夹名称 (例如，符号) 也可以用作文件共享名称和虚拟目录名称。 如果要添加新的符号存储区，将在 D： SymStore 下创建一个新的子文件夹， \\ 并将此名称的新文件共享和虚拟目录公开给客户端。

应仔细选择文件夹树的位置以及磁盘的文件系统。 当缓存 (内部) 生成服务器和 Internet 中的文件时，符号存储区会获得极大的 (tb) 。 文件夹树应驻留在能够进行大量读取和大量写入操作的磁盘上。 文件系统可能会影响性能，ReFS 的性能可能优于 NTFS 并且应调查大型部署。 同样，与服务器之间的网络连接速度应足以处理来自客户端的负载，同时还应为上游符号存储的负载，以检索缓存填充的符号。

## <a name="span-idsymbol_store_single-tier_or_two-tier_structurespanspan-idsymbol_store_single-tier_or_two-tier_structurespanspan-idsymbol_store_single-tier_or_two-tier_structurespansymbol-store-single-tier-or-two-tier-structure"></a><span id="Symbol_Store_Single-Tier_or_Two-Tier_Structure"></span><span id="symbol_store_single-tier_or_two-tier_structure"></span><span id="SYMBOL_STORE_SINGLE-TIER_OR_TWO-TIER_STRUCTURE"></span>符号存储区 Single-Tier 或 Two-Tier 结构


通常，文件位于单个层目录结构中，其中缓存的每个文件都有一个子目录。 在每个文件名文件夹下，会创建其他文件夹来存储文件的每个版本。 树将具有以下结构：

```console
D:\SymStore\Symbols\ntdll.dll\...\
D:\SymStore\Symbols\ntdll.pdb\...\
D:\SymStore\Symbols\kernel32.dll\...\
D:\SymStore\Symbols\kernel32.pdb\...\
```

如果要存储大量文件，则可以在符号存储区的根使用双层结构。 文件名的前两个字母用作中间文件夹名称。

若要使用双层结构，请将名为 index2.txt 的文件放在 D： SymStore 符号的根目录中 \\ \\ 。 文件的内容并不重要。 如果此文件存在，symsrv.dll 将使用以下结构创建并使用两层树中的文件：

```console
D:\SymStore\Symbols\nt\ntdll.dll\...\
D:\SymStore\Symbols\nt\ntdll.pdb\...\
D:\SymStore\Symbols\ke\kernel32.dll\...\
D:\SymStore\Symbols\ke\kernel32.pdb\...\
```

如果要在填充符号存储区后转换结构，请使用调试器文件夹中的 convertstore.exe 应用程序。 若要允许该工具正常工作，请在根文件夹中创建一个名为000Admin 的文件夹。 此文件夹是 convertstore.exe 必需的，因此它可以控制对符号存储区的锁定。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[HTTP 符号存储](http-symbol-stores.md)

[文件共享 (SMB) 符号服务器](file-share--smb--symbol-server.md)

 

 






