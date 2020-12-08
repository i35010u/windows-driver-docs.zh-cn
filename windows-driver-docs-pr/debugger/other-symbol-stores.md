---
title: 其他符号存储
description: 其他符号存储
keywords:
- 符号存储区，编写自己的符号存储区
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 57c97fb026893b20dbfac623a5145fc6198b83fa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788767"
---
# <a name="other-symbol-stores"></a>其他符号存储


## <span id="ddk_using_other_symbol_stores_dbg"></span><span id="DDK_USING_OTHER_SYMBOL_STORES_DBG"></span>


可以编写自己的符号存储创建程序，而不是使用 SymStore。

由于 SymStore 事务全部记录在 CSV 格式的文本文件中，因此您可以利用任何现有的 SymStore 日志文件，以便在自己的数据库程序中使用。

如果你计划使用随 Windows 包调试工具提供的 SymSrv 程序，则建议你也使用 SymStore。 这两个程序的更新将始终一起发布，因此它们的版本将始终匹配。

 

 





