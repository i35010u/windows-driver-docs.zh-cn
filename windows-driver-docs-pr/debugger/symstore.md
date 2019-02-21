---
title: SymStore
description: SymStore
ms.assetid: acc7bf3a-62ea-4c93-843e-b81d4f71555f
keywords:
- SymStore 功能
- SymStore，使用
- 符号存储区，SymStore (symstore.exe)
ms.date: 03/27/2018
ms.localizationpriority: medium
ms.openlocfilehash: e22cad6b6b3bd3967a8b3148bbee3dcb73935653
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524950"
---
# <a name="symstore"></a>SymStore


## <span id="ddk_using_symstore_dbg"></span><span id="DDK_USING_SYMSTORE_DBG"></span>


SymStore (symstore.exe) 是用于创建符号存储区的工具。 它包含在调试工具的 Windows 中。 有关详细信息，请参阅[的 Windows 中下载调试的工具](https://docs.microsoft.com/windows-hardware/drivers/debugger/debugger-download-tools)。

SymStore 使调试器能够查找基于时间戳和大小的图像 （.dbg 或可执行文件） 或签名和期限 （用于.pdb 文件） 的符号的格式存储的符号。 在符号存储区对传统符号存储格式的优点是，可以存储或在同一台服务器上引用并且无需任何事先了解调试器来检索所有符号的哪一种产品包含相应的符号。

请注意，不能在同一服务器上存储多个版本的.pdb 符号文件 （例如，公共和专用版本），这是因为它们每个包含相同的签名和年龄。

本部分包括：

[SymStore 事务](symstore-transactions.md)

[文件系统引用和符号文件](file-system-references-and-symbol-files.md)

[SymStore 压缩文件](symstore-compressed-files.md)

[符号存储格式](symbol-storage-format.md)

 

 





