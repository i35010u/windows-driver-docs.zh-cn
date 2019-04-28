---
title: 示例 2 使用标志缩写设置一个标志
description: 示例 2 使用标志缩写设置一个标志
ms.assetid: 3c011ca5-8901-4bf2-b95d-364d644cb476
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: b4a3d2e7cff878921886a0b93bfa9ed6db721345
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347724"
---
# <a name="example-2-setting-a-flag-by-using-a-flag-abbreviation"></a>示例 2：使用标志缩写设置标志


## <span id="ddk_example_2___setting_a_flag_by_using_a_flag_abbreviation_dtools"></span><span id="DDK_EXAMPLE_2___SETTING_A_FLAG_BY_USING_A_FLAG_ABBREVIATION_DTOOLS"></span>


下面的命令集[显示加载程序快照](show-loader-snaps.md)notepad.exe 图像文件的标志。 **显示加载程序将对齐**采用加载过程中，捕获地加载和卸载的可执行映像和其支持的库模块的快照。

该命令使用 **/i**参数来指示图像文件模式，它指定图像文件 notepad.exe 的名称。 若要标识该标志，该命令使用**sls**的缩写形式**显示加载程序对齐**，它位于使用加号 （+） 以指示已设置的标志的缩写形式。 而无需加号，该命令不起作用。

```console
gflags /i notepad.exe +sls 
```

在响应中，用 GFlags 显示设置为 notepad.exe 的标志。 显示表示该命令成功。 **显示加载程序对齐**所有新会话的记事本程序启用功能。

```console
Current Registry Settings for notepad.exe executable are: 00000002
    sls - Show Loader Snaps
```

 

 





