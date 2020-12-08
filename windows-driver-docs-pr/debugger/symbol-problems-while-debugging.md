---
title: 调试时的符号问题
description: 调试时的符号问题
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c7c686edf6c7405b1ca8f821f91af9184a091b1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834683"
---
# <a name="symbol-problems-while-debugging"></a>调试时的符号问题


## <span id="ddk_debugging_user_mode_processes_without_symbols_dbg"></span><span id="DDK_DEBUGGING_USER_MODE_PROCESSES_WITHOUT_SYMBOLS_DBG"></span>


无效或缺失的符号是调试器问题的最常见原因之一。 出现某种问题时，您需要找出是否存在符号问题。

在某些情况下，解决方案需要获取正确的符号文件。 在其他情况下，只需重新配置调试器即可识别已有的符号文件。 但如果无法获取正确的符号文件，则需要解决此问题，并以更有限的方式调试目标。

本节包括：

[验证符号](verifying-symbols.md)

[匹配符号名称](matching-symbol-names.md)

[读取移出页面的标头中的符号](reading-symbols-from-paged-out-headers.md)

[将 PEB 移出页面时映射符号](mapping-symbols-when-the-peb-is-paged-out.md)

[不使用符号调试用户模式进程](debugging-user-mode-processes-without-symbols.md)

[调试性能优化的代码](debugging-performance-optimized-code.md)

 

 





