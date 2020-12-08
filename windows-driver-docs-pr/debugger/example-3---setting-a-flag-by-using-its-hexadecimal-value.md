---
title: 示例3：使用其十六进制值设置标志
description: 示例3：使用其十六进制值设置标志
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 024be116fc4acae9fd2c10360c8c75cd89fe6817
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838523"
---
# <a name="example-3-setting-a-flag-by-using-its-hexadecimal-value"></a>示例3：使用其十六进制值设置标志


## <span id="ddk_example_3___setting_a_flag_by_using_its_hexadecimal_value_dtools"></span><span id="DDK_EXAMPLE_3___SETTING_A_FLAG_BY_USING_ITS_HEXADECIMAL_VALUE_DTOOLS"></span>


以下命令将设置系统范围的 [启用页堆](enable-page-heap.md) 标志。 **启用页堆** 将保护页和其他跟踪功能添加到每个堆分配。

该命令使用 **/r** 参数来指示系统范围内的注册表模式。 为了识别标志，该命令使用 **2000000**，它表示0x2000000，这是 **启用页堆** 的十六进制值。

尽管该命令设置了标志，但它省略了加号 (+) 符号。 使用十六进制值时，符号是可选的，并添加 (+) 为默认值。

```console
gflags /r 2000000 
```

在响应中，GFlags 显示注册表中设置的系统范围内的标志。 该显示指示该命令已成功。 Windows 重新启动时，将为所有进程启用 " **启用页堆** " 功能。

```console
Current Boot Registry Settings are: 02000000
    hpa - Enable page heap
```

 

 





