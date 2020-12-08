---
title: 文件系统参考和符号文件
description: 文件系统参考和符号文件
keywords:
- SymStore，短文件名
- 短文件名和 SymStore
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5b40ccaf631788d37752f9e5453fe626710a225
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838201"
---
# <a name="file-system-references-and-symbol-files"></a>文件系统参考和符号文件


## <span id="ddk_symbol_files_overview_dbg"></span><span id="DDK_SYMBOL_FILES_OVERVIEW_DBG"></span>


磁盘上的文件可以包含长文件名，并自动生成缩写的 MS-DOS 兼容8.3 短文件名。 将符号文件添加到符号存储区后，如果符号文件包含任何缩写的 MS-DOS 8.3 文件名，则在调试过程中可能无法访问该符号文件中的符号。

当工具创建符号文件时，在符号文件调试记录中记录的文件名的版本取决于工具及其运行方式。 如果符号文件具有缩写的 MS-DOS 8.3 文件名，而不是嵌入在记录中的实际文件名，则在调试时加载符号可能会遇到问题，因为缩写的文件名因系统而异。 如果出现此问题，则在调试过程中可能无法访问这些符号文件的内容。 如果可能，用户应在创建符号文件时避免使用缩写的文件路径名。 无意中使用缩写文件名的一些方法是使用文件的缩写路径名称、 *包含* 目录或包含的库文件。

有关详细信息，请参阅 [匹配符号名称](matching-symbol-names.md)。

 

 





