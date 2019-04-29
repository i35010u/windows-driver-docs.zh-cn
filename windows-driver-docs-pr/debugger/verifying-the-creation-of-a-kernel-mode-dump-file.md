---
title: 验证是否已创建内核模式转储文件
description: 验证是否已创建内核模式转储文件
ms.assetid: ea1dc18d-8974-4de8-accd-1cbc515d71d0
keywords:
- 转储文件，验证创建内核模式转储
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a372db165443b67b14a3e88722fd389a9968b551
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63386436"
---
# <a name="verifying-the-creation-of-a-kernel-mode-dump-file"></a>验证是否已创建内核模式转储文件


## <span id="ddk_verifying_the_creation_of_a_kernel_mode_dump_file_dbg"></span><span id="DDK_VERIFYING_THE_CREATION_OF_A_KERNEL_MODE_DUMP_FILE_DBG"></span>


如果计算机已中断到调试器，但您不确定是否已成功写入崩溃转储文件，执行以下命令：

```dbgcmd
dd nt!IopFinalCrashDumpStatus L1
```

这将显示的值**IopFinalCrashDumpStatus**变量。

如果此值等于零，则过程成功。 如果它等于-1 (0xFFFFFFFF)，转储进程未启动。

任何其他值是在转储过程中表示错误的错误状态代码。

 

 





