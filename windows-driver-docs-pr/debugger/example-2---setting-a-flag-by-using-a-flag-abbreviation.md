---
title: 示例2：使用标志缩写设置标志
description: 示例2：使用标志缩写设置标志
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: d878f0fef57404311e17029a26516aadfa6e55e9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840443"
---
# <a name="example-2-setting-a-flag-by-using-a-flag-abbreviation"></a>示例2：使用标志缩写设置标志


## <span id="ddk_example_2___setting_a_flag_by_using_a_flag_abbreviation_dtools"></span><span id="DDK_EXAMPLE_2___SETTING_A_FLAG_BY_USING_A_FLAG_ABBREVIATION_DTOOLS"></span>


以下命令将设置 notepad.exe 映像文件的 " [显示加载程序" 对齐](show-loader-snaps.md) 标志。 **显示加载程序 snap** 获取加载过程的快照，详细捕获可执行映像的加载和卸载及其支持的库模块。

该命令使用 **/i** 参数来指示图像文件模式，并指定 notepad.exe 的图像文件的名称。 为了识别标志，该命令使用了 **sls**， **显示加载程序** 的缩写，并在缩写前面加上符号 (+) ，以指示设置了标志。 如果没有加号，则该命令不起作用。

```console
gflags /i notepad.exe +sls 
```

在响应中，GFlags 显示为 notepad.exe 设置的标志。 该显示指示该命令已成功。 为记事本程序的所有新会话启用了 " **显示加载程序" 快照** 功能。

```console
Current Registry Settings for notepad.exe executable are: 00000002
    sls - Show Loader Snaps
```

 

 





