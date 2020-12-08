---
title: 示例4设置多个标志
description: 示例4设置多个标志
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 01f77555926525ce81fc68ad0a36cbfb11138644
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838521"
---
# <a name="example-4-setting-multiple-flags"></a>示例4：设置多个标志


## <span id="ddk_example_4___setting_multiple_flags_dtools"></span><span id="DDK_EXAMPLE_4___SETTING_MULTIPLE_FLAGS_DTOOLS"></span>


以下命令为当前会话设置这三个标志：

-   启用 (hfc、0x20) 的[堆免费检查](enable-heap-free-checking.md)

-   启用 (hpc、0x40) 的[堆参数检查](enable-heap-parameter-checking.md)

-   对调用 (hvc，0x80) [启用堆验证](enable-heap-validation-on-call.md)

此命令使用 **/k** 参数指定仅)  (会话的内核模式。 它将内核模式的值设置为 **E0** (0xE0) ，所选标志的十六进制值的总和 (0x20 + 0x40 + 0x80) 。

```console
gflags /k e0 
```

在响应中，GFlags 显示为会话设置的标志的修订值。 此显示指示命令成功，并设置了命令中指定的三个标志。

```console
Current Running Kernel Settings are: 000000e0
    hfc - Enable heap free checking
    hpc - Enable heap parameter checking
    hvc - Enable heap validation on call
```

可以使用多个不同的 GFlags 命令来设置标志。 以下每个命令都与此示例中使用的命令具有相同的效果，并且可以互换使用这些方法：

```console
gflags /k +20 +40 +80 
gflags /k +E0 
gflags /k +hfc +hpc +hvc 
```

内核 (运行时) 标志立即生效，且在关闭 Windows 之前仍然有效。

 

 





