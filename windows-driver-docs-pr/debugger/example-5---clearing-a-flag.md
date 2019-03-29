---
title: 示例 5 清除标志
description: 示例 5 清除标志
ms.assetid: 63c8bae9-ae6e-4d82-9389-ec36554635ab
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: d0de0975e41bc5452ececcc237f83a2cfa605398
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562507"
---
# <a name="example-5-clearing-a-flag"></a>示例 5：清除标志


## <span id="ddk_example_5___clearing_a_flag_dtools"></span><span id="DDK_EXAMPLE_5___CLEARING_A_FLAG_DTOOLS"></span>


以下命令可清除系统级[启用页堆](enable-page-heap.md)标志在注册表中的设置。 该命令使用 **/r**参数来指示整个系统注册表模式并**hpa**的缩写形式**启用页堆**标志。 减号 （-） 表示的标志是要清除。

```console
gflags /r -hpa 
```

在响应中，用 GFlags 显示整个系统的注册表项的当前值。 显示指示命令成功，而且将不再任何标志集。

```console
Current Boot Registry Settings are: 00000000 
```

请注意，以下命令，使用的十六进制值**启用页堆**标志，此示例中使用该命令的效果相同。 这些命令可以互换使用：

```console
gflags /r -02000000 
```

 

 





