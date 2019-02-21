---
title: 符号进行调试时的问题
description: 符号进行调试时的问题
ms.assetid: 2713c371-9683-4d0d-a8ab-8a4c897ba0ab
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cc7b959d45d576368aa37c4d6d3dfef6db3714a0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544468"
---
# <a name="symbol-problems-while-debugging"></a>符号进行调试时的问题


## <span id="ddk_debugging_user_mode_processes_without_symbols_dbg"></span><span id="DDK_DEBUGGING_USER_MODE_PROCESSES_WITHOUT_SYMBOLS_DBG"></span>


无效或缺失的符号是调试器问题的最常见原因之一。 当您看到的某种类型的问题时，您需要了解是否有一个符号的问题。

在某些情况下，该解决方案涉及到获取正确的符号文件。 在其他情况下，只需重新配置调试器以识别已有的符号文件。 但如果您不能获取正确的符号文件，则需要解决此问题和限制更多的方式调试目标。

本部分包括：

[验证符号](verifying-symbols.md)

[匹配的符号名称](matching-symbol-names.md)

[调出标头中读取符号](reading-symbols-from-paged-out-headers.md)

[映射符号时 PEB 将分页输出](mapping-symbols-when-the-peb-is-paged-out.md)

[调试用户模式进程，而无需符号](debugging-user-mode-processes-without-symbols.md)

[调试性能优化的代码](debugging-performance-optimized-code.md)

 

 





