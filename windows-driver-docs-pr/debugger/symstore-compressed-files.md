---
title: SymStore 压缩文件
description: SymStore 压缩文件
ms.assetid: 4ec6a7f5-ceee-46d5-9a5e-36ab9fe9db52
keywords:
- SymStore，压缩文件
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 401e1d86c46436bb21639ea4fe60845003973ddc
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84533920"
---
# <a name="symstore-compressed-files"></a>SymStore 压缩文件


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


可以通过两种不同的方式将 SymStore 用于压缩的文件：

1.  使用带有 **/p**选项的 SymStore 存储指向符号文件的指针。 SymStore 完成后，压缩指针所指向的文件。

2.  使用带有 **/x**选项的 SymStore 创建索引文件。 SymStore 完成后，压缩索引文件中列出的文件。 然后，使用 SymStore 和 **/y**选项（如果需要，还可以使用 **/p**选项）将文件或指针存储到符号存储区中的文件。 （SymStore 不需要对文件进行解压缩即可执行此操作。）

符号服务器将负责在正确的时间解压缩文件。

如果使用 SymSrv 作为符号服务器，则应使用[此处](https://www.microsoft.com/download/details.aspx?displaylang=en&id=17657 )提供的 "压缩 .exe" 工具完成任何压缩。 压缩的文件应将一个下划线作为其文件扩展名中的最后一个字符（例如，module1 \_ 或 module2 \_ ）。 有关详细信息，请参阅[SymSrv](symsrv.md)。

 

 





