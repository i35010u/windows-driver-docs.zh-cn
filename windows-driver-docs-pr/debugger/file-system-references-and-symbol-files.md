---
title: 文件系统参考和符号文件
description: 文件系统参考和符号文件
ms.assetid: c667380f-2942-453c-9ec8-70d3e1355e72
keywords:
- SymStore，短文件名
- 短文件名和 SymStore
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d079eda2b815270ee37f367a9fcb6b7262fd855
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380617"
---
# <a name="file-system-references-and-symbol-files"></a>文件系统参考和符号文件


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


磁盘上的文件可以同时具有长文件名和自动生成缩写的 MS-DOS 兼容 8.3 短文件名。 将符号文件添加到符号存储区之后, 就可以，在该符号文件中的符号可能无法访问在调试期间如果符号文件包含任何缩写的 MS-DOS 8.3 文件名称。

当这些工具创建的符号文件时，文件名称的符号文件调试记录中记录的版本取决于的工具和运行方式。 如果符号文件而不是嵌入在记录中的实际文件名称的缩写的 MS-DOS 8.3 文件名称，在调试时加载的符号可能会遇到问题，因为缩写的文件名不同系统之间。 如果出现此问题，这些符号文件的内容在调试期间可能无法访问。 只要有可能，用户应避免在创建符号文件时使用缩写的文件路径名称。 无意中使用缩写的文件的名称的一些方法，则在使用源文件中，缩写的文件路径名*包括*目录或一个包含的库文件。

有关详细信息，请参阅[匹配的符号名](matching-symbol-names.md)。

 

 





