---
title: 验证是否已创建内核模式转储文件
description: 验证是否已创建内核模式转储文件
keywords:
- 转储文件，验证内核模式转储创建
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b4c65e4bb068d8f054c53c313e7a85ddcc71771
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802967"
---
# <a name="verifying-the-creation-of-a-kernel-mode-dump-file"></a>验证是否已创建内核模式转储文件


## <span id="ddk_verifying_the_creation_of_a_kernel_mode_dump_file_dbg"></span><span id="DDK_VERIFYING_THE_CREATION_OF_A_KERNEL_MODE_DUMP_FILE_DBG"></span>


如果计算机已中断到调试器，但不确定是否已成功写入故障转储文件，请执行以下命令：

```dbgcmd
dd nt!IopFinalCrashDumpStatus L1
```

这会显示 **IopFinalCrashDumpStatus** 变量的值。

如果此值等于零，则此过程已成功完成。 如果它等于-1 (0xFFFFFFFF) ，则转储过程尚未开始。

任何其他值是指示转储过程中的错误的状态代码。

 

 





