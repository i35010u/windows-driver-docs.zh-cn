---
title: 示例 3 使用十六进制值设置一个标志
description: 示例 3 使用十六进制值设置一个标志
ms.assetid: 64fa0b2e-9fe7-47d0-bf83-8ae7c06252b6
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8ca853bd3c788025563a5ca358e9d1570605f225
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569456"
---
# <a name="example-3-setting-a-flag-by-using-its-hexadecimal-value"></a>示例 3：使用标志的十六进制值设置标志


## <span id="ddk_example_3___setting_a_flag_by_using_its_hexadecimal_value_dtools"></span><span id="DDK_EXAMPLE_3___SETTING_A_FLAG_BY_USING_ITS_HEXADECIMAL_VALUE_DTOOLS"></span>


以下命令设置系统级[启用页堆](enable-page-heap.md)标志。 **启用页堆**将保护页并且将其他跟踪功能添加到每个堆分配。

该命令使用 **/r**参数以指示整个系统注册表模式。 若要标识该标志，该命令使用**2000000**，它表示 0x2000000 的十六进制值**启用页堆**。

尽管该命令设置一个标志，它会省略加号 （+） 登录。 当使用的十六进制值，符号是可选的加号 （+） 是默认值。

```console
gflags /r 2000000 
```

在响应中，用 GFlags 显示在注册表中设置的系统范围内标志。 显示表示该命令成功。 **启用页堆**Windows 重新启动时，将为所有进程启用功能。

```console
Current Boot Registry Settings are: 02000000
    hpa - Enable page heap
```

 

 





