---
title: 示例5清除标志
description: 示例5清除标志
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: f0e826c29a32fa181001ae549e2531fc806e1645
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840441"
---
# <a name="example-5-clearing-a-flag"></a>示例5：清除标志


## <span id="ddk_example_5___clearing_a_flag_dtools"></span><span id="DDK_EXAMPLE_5___CLEARING_A_FLAG_DTOOLS"></span>


以下命令清除在注册表中设置的系统范围内 [启用页堆](enable-page-heap.md) 标志。 该命令使用 **/r** 参数来指示系统范围内的注册表模式和 **hpa**，这是 " **启用页堆** 标志" 的缩写。 减号 (-) 指示清除标志。

```console
gflags /r -hpa 
```

在响应中，GFlags 显示系统范围注册表项的当前值。 此显示指示该命令已成功完成，并且不再有任何标志集。

```console
Current Boot Registry Settings are: 00000000 
```

请注意，以下使用 " **启用页堆** 标志" 的十六进制值的命令与本示例中使用的命令具有相同的效果。 可以交换使用以下命令：

```console
gflags /r -02000000 
```

 

 





