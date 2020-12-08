---
title: SymStore
description: SymStore
keywords:
- SymStore，功能
- SymStore，使用
- '符号存储，SymStore ( # A0) '
ms.date: 03/27/2018
ms.localizationpriority: medium
ms.openlocfilehash: 29d99077a49d85bfa47bb83175b05e1d41a8ebc6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813925"
---
# <a name="symstore"></a>SymStore


## <span id="ddk_using_symstore_dbg"></span><span id="DDK_USING_SYMSTORE_DBG"></span>

SymStore ( # A0) 是用于创建符号存储区的工具。 它包含在适用于 Windows 的调试工具中。 有关详细信息，请参阅 [下载适用于 Windows 的调试工具](debugger-download-tools.md)。

SymStore 以一种格式存储符号，使调试器能够根据) 的文件 (的时间戳和大小以及 .pdb 文件) 的签名和 age (来查找符号。 符号存储区与传统符号存储格式的优点是，可以在同一台服务器上存储或引用所有符号，并由调试器检索，而不需要事先了解哪些产品包含相应的符号。

请注意， (的 .pdb 符号文件的多个版本（例如，公共和私有版本) 无法存储在同一服务器上，因为它们每个都包含相同的签名和期限。

本节包括：

[SymStore 事务](symstore-transactions.md)

[文件系统参考和符号文件](file-system-references-and-symbol-files.md)

[符号存储格式](symbol-storage-format.md)

 

 





