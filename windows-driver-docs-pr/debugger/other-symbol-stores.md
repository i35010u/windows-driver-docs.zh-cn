---
title: 其他符号存储
description: 其他符号存储
ms.assetid: 65bb4291-c56a-4837-ac45-6751ebdbd579
keywords:
- 符号存储区，编写您自己符号存储区
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc2863c2ad0614c9b889712c39936e316724b618
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331261"
---
# <a name="other-symbol-stores"></a>其他符号存储


## <span id="ddk_using_other_symbol_stores_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_STORES_DBG"></span>


可以编写自己的符号存储区创建程序，而不是使用 SymStore 它。

由于所有记录中文本文件的 CSV 格式 SymStore 事务，因此可以利用使用任何现有 SymStore 日志文件，数据库程序中。

如果你打算使用与为 Windows 调试工具程序包提供程序，建议的 SymSrv 也使用 SymStore。 发布更新，这两个程序将始终在一起，并因此将始终匹配其版本。

 

 





