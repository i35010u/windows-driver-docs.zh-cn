---
title: SymStore
description: SymStore
ms.assetid: acc7bf3a-62ea-4c93-843e-b81d4f71555f
keywords:
- SymStore，功能
- SymStore，使用
- 符号存储，SymStore （SymStore）
ms.date: 03/27/2018
ms.localizationpriority: medium
ms.openlocfilehash: 46c8feeeac0d3c7a1b7e42a2d143f162bb11de47
ms.sourcegitcommit: dadc9ced1670d667e31eb0cb58d6a622f0f09c46
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84534288"
---
# <a name="symstore"></a>SymStore


## <span id="ddk_using_symstore_dbg"></span><span id="DDK_USING_SYMSTORE_DBG"></span>


SymStore （SymStore）是用于创建符号存储区的工具。 它包含在适用于 Windows 的调试工具中。 有关详细信息，请参阅[下载适用于 Windows 的调试工具](debugger-download-tools.md)。

SymStore 以一种格式存储符号，使调试器可以根据图像的时间戳和大小（dbg 或可执行文件）或签名和 age （对于 .pdb 文件）来查找符号。 符号存储区与传统符号存储格式的优点是，可以在同一台服务器上存储或引用所有符号，并由调试器检索，而不需要事先了解哪些产品包含相应的符号。

请注意，不能在同一服务器上存储 .pdb 符号文件的多个版本（例如，公共版本和私有版本），因为它们每个版本都包含相同的签名和生存期。

本节包括：

[SymStore 事务](symstore-transactions.md)

[文件系统参考和符号文件](file-system-references-and-symbol-files.md)

[SymStore 压缩文件](symstore-compressed-files.md)

[符号存储格式](symbol-storage-format.md)

 

 





