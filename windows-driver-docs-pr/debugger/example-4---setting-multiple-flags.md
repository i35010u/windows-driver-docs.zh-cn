---
title: 示例 4 设置多个标志
description: 示例 4 设置多个标志
ms.assetid: b8c7301b-4a34-4f03-8c5e-ba43a1fb3681
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: e11c0db223385480076b1aea7d84458541516dc4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56534557"
---
# <a name="example-4-setting-multiple-flags"></a>示例 4:设置多个标志


## <span id="ddk_example_4___setting_multiple_flags_dtools"></span><span id="DDK_EXAMPLE_4___SETTING_MULTIPLE_FLAGS_DTOOLS"></span>


以下命令将这三个标识设置为当前会话中：

-   [启用堆免费检查](enable-heap-free-checking.md)(hfc，0x20)

-   [启用堆参数检查](enable-heap-parameter-checking.md)(hpc，0x40)

-   [启用在调用堆验证](enable-heap-validation-on-call.md)(hvc，0x80)

此命令使用 **/k**参数来指定内核模式 （仅会话）。 设置到内核模式的值**E0** (0xE0)、 所选标志 (0x20 + 0x40 + 0x80) 的十六进制值的总和。

```console
gflags /k e0 
```

在响应中，用 GFlags 显示为会话设置的标志的修订的值。 显示指示命令成功，而且设置三个命令中指定的标记。

```console
Current Running Kernel Settings are: 000000e0
    hfc - Enable heap free checking
    hpc - Enable heap parameter checking
    hvc - Enable heap validation on call
```

可以使用多个不同的 GFlags 命令来设置标志。 每个以下的命令有与在此示例中所使用的命令相同的效果，并且可以互换使用方法：

```console
gflags /k +20 +40 +80 
gflags /k +E0 
gflags /k +hfc +hpc +hvc 
```

内核 （运行时间） 标志会立即生效，Windows 关闭之前保持有效。

 

 





