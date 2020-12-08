---
title: 示例1显示全局标志
description: 示例1显示全局标志
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: beeb73d407eaf5148ed6a802c3776bc9f31fff87
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829731"
---
# <a name="example-1-displaying-global-flags"></a>示例1：显示全局标志


## <span id="ddk_example_1___displaying_global_flags_dtools"></span><span id="DDK_EXAMPLE_1___DISPLAYING_GLOBAL_FLAGS_DTOOLS"></span>


本示例中演示的命令显示在注册表中设置了系统范围内的标志，为会话 (内核模式) 设置了系统标记，并显示了为映像文件设置的标志。

下面的 GFlags 命令显示在注册表中设置的系统范围内标志的当前值。 它使用 **/r** 参数来指定系统范围的注册表项。

```console
gflags /r 
```

在响应中，GFlags 显示一个十六进制值，该值表示所有标志集的总和和标志集的列表。

```console
Current Boot Registry Settings are: 40001400
    ptg - Enable pool tagging
    ust - Create user mode stack trace database
    bhd - Enable bad handles detection
```

在此示例中，结果显示有三个标记集，组合值为0x40001400。

-   [启用池标记](enable-pool-tagging.md) (ptg) = 0x400

-   [创建用户模式堆栈跟踪数据库](create-user-mode-stack-trace-database.md) (ust) = 0x1000

-   [启用错误的句柄检测](enable-bad-handles-detection.md) (bhd) = 0x40000000

以下命令显示为当前会话设置的标志。 它使用 **/k** 参数来指示内核模式。

```console
gflags /k 
```

以下命令显示 notepad.exe 的图像文件的注册表中设置的标志。 它使用 **/i** 参数来指示图像文件模式并指定映像文件。

```console
gflags /i notepad.exe 
```

请记住，显示的标志值可能不是当前的有效标志值。 在重新启动 Windows 之前，系统范围内标志的更改将不会生效。 在重新启动程序之前，对图像文件标志设置的更改将不会生效。

 

 





