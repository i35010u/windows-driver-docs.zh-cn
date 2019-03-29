---
title: 符号存储文件夹树
description: 支持 SMB 和 HTTP 请求在符号存储区是驻留在本地磁盘上的文件夹树。
ms.assetid: AB23A180-71C3-4EBE-A3DE-765D264EF130
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: b25b29a516c09eab1232b66df7416c5dd439b29d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566076"
---
# <a name="symbol-store-folder-tree"></a>符号存储文件夹树


支持 SMB 和 HTTP 请求在符号存储区是驻留在本地磁盘上的文件夹树。

为了简化管理，子文件夹名称 （例如符号） 也可用作文件共享名称，还将虚拟目录名称。 如果要添加新的符号存储区，将进行新的子文件夹下 d:\\SymStore，以及新的文件共享和该名称的虚拟目录将进行公开给客户端的存储。

应慎重选择文件夹树的位置，以及磁盘的文件系统。 从 （内部） 的缓存文件的生成服务器和 Internet 时，符号存储区可以获得极大 （兆兆字节）。 文件夹树应驻留的大量读取和写入数少能够在磁盘上。 文件系统可能会影响性能-ReFS 可以更好地低于 NTFS，应调查对于大型部署。 同样，网络连接到服务器应以处理来自客户端负载的足够速度的并且还加载到上游符号存储区检索缓存填充的符号。

## <a name="span-idsymbolstoresingle-tierortwo-tierstructurespanspan-idsymbolstoresingle-tierortwo-tierstructurespanspan-idsymbolstoresingle-tierortwo-tierstructurespansymbol-store-single-tier-or-two-tier-structure"></a><span id="Symbol_Store_Single-Tier_or_Two-Tier_Structure"></span><span id="symbol_store_single-tier_or_two-tier_structure"></span><span id="SYMBOL_STORE_SINGLE-TIER_OR_TWO-TIER_STRUCTURE"></span>符号存储区的单层或两层结构


通常情况下文件放置在单个层内的目录结构的单个子目录所在缓存每个文件名。 每个文件名在文件夹下，进行的其他文件夹来存储每个版本的文件。 在树将具有此结构：

```console
D:\SymStore\Symbols\ntdll.dll\...\
D:\SymStore\Symbols\ntdll.pdb\...\
D:\SymStore\Symbols\kernel32.dll\...\
D:\SymStore\Symbols\kernel32.pdb\...\
```

如果大量的文件存储，两层结构可以使用符号存储区的根目录中。 文件名的前 2 个字母用作中间文件夹名称。

若要使用的两层结构，将文件根目录中的 d： 调用 index2.txt\\SymStore\\符号。 文件的内容是不重要。 此文件存在时，symsrv.dll 将创建和使用两层树中使用此结构中的文件：

```console
D:\SymStore\Symbols\nt\ntdll.dll\...\
D:\SymStore\Symbols\nt\ntdll.pdb\...\
D:\SymStore\Symbols\ke\kernel32.dll\...\
D:\SymStore\Symbols\ke\kernel32.pdb\...\
```

如果你想要将结构转换填充符号存储区之后，调试器文件夹中使用 convertstore.exe 应用程序。 若要允许若要运行该工具，创建一个名为 000Admin 根文件夹中。 Convertstore.exe 需要此文件夹，以便它可以控制在符号存储区的锁定。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[HTTP 符号存储区](http-symbol-stores.md)

[文件共享 (SMB) 符号服务器](file-share--smb--symbol-server.md)

 

 






