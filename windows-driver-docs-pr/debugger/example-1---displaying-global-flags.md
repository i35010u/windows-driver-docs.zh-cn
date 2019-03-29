---
title: 示例 1 显示全局标志
description: 示例 1 显示全局标志
ms.assetid: c1a1eafd-d70a-43f9-af90-33ddc33758fe
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: a635b2bfa7f0cb6b7f627f207564263c1a4ed3da
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562624"
---
# <a name="example-1-displaying-global-flags"></a>示例 1：显示全局标志


## <span id="ddk_example_1___displaying_global_flags_dtools"></span><span id="DDK_EXAMPLE_1___DISPLAYING_GLOBAL_FLAGS_DTOOLS"></span>


在注册表中设置的系统范围内标志、 系统标志已设置为会话 （内核模式） 和设置的图像文件的标志，在此示例显示中所示命令。

下面的 GFlags 命令显示在注册表中设置的系统范围内标志的当前值。 它使用 **/r**参数来指定整个系统的注册表项。

```console
gflags /r 
```

在响应中，用 GFlags 显示单个的十六进制值表示的标志集的列表和设置了所有标志的之和。

```console
Current Boot Registry Settings are: 40001400
    ptg - Enable pool tagging
    ust - Create user mode stack trace database
    bhd - Enable bad handles detection
```

在此示例中，结果显示，有三个标记设置，请使用 0x40001400 合并值。

-   [启用标记池](enable-pool-tagging.md)(ptg) = 0x400

-   [创建用户模式堆栈跟踪数据库](create-user-mode-stack-trace-database.md)(ust) = 0x1000

-   [启用错误句柄检测](enable-bad-handles-detection.md)(bhd) = 0x40000000

下面的命令显示当前会话设置的标志。 它使用 **/k**参数来指示内核模式。

```console
gflags /k 
```

下面的命令显示注册表中的图像文件 notepad.exe 的标志集。 它使用 **/i**参数来指示图像文件模式，它指定图像文件。

```console
gflags /i notepad.exe 
```

请记住，显示的标志值可能不是当前有效的标志值。 重新启动 Windows，更改系统范围内标志才有效。 重新启动该程序，对图像文件标志设置的更改才有效。

 

 





