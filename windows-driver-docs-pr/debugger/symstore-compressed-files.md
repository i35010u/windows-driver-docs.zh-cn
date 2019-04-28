---
title: SymStore 压缩文件
description: SymStore 压缩文件
ms.assetid: 4ec6a7f5-ceee-46d5-9a5e-36ab9fe9db52
keywords:
- SymStore，压缩文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22ad34cdb4e93e6d9376f0870e33543c2bfa2804
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63335459"
---
# <a name="symstore-compressed-files"></a>SymStore 压缩文件


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


两个不同的方式，可以使用压缩文件使用 SymStore:

1.  使用与 SymStore **/p**选项以便存储指向符号文件。 SymStore 完成后，压缩指针引用的文件。

2.  使用与 SymStore **/x**选项来创建索引文件。 SymStore 完成后，压缩索引文件中列出的文件。 然后，使用与 SymStore **/y**选项 (并且，如果你想 **/p**选项) 在符号存储区中存储的文件或文件的指针。 （SymStore 不需要解压缩文件来执行此操作。）

符号服务器将负责在适当的时候解压缩文件。

如果使用的 SymSrv 作为符号服务器，应完成任何压缩使用 compress.exe 工具可[此处](https://go.microsoft.com/fwlink/p/?linkid=239917)。 压缩的文件应具有其文件扩展名中的最后一个字符与下划线 (例如，module1.pd\_或 module2.db\_)。 有关详细信息，请参阅[SymSrv](symsrv.md)。

 

 





