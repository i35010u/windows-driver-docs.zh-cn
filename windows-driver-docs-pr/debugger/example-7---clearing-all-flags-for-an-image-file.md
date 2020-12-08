---
title: 示例7清除映像文件的所有标志
description: 示例7清除映像文件的所有标志
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 15611e059d8f078b9dd371d3b73bf0961577e7dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838227"
---
# <a name="example-7-clearing-all-flags-for-an-image-file"></a>示例7：清除映像文件的所有标志


## <span id="ddk_example_7___clearing_all_flags_for_an_image_file_dtools"></span><span id="DDK_EXAMPLE_7___CLEARING_ALL_FLAGS_FOR_AN_IMAGE_FILE_DTOOLS"></span>


以下命令将清除映像文件的所有标志和图像调试器选项。 命令将值 (0xFFFFFFFF) 添加到当前标志值。 GFlags 通过删除映像文件的 **GlobalFlag** 注册表项来做出响应，从而删除它存储的所有值。

此命令不会影响在系统范围的 **GlobalFlag** 注册表项中设置的标志，也不会影响 (内核模式) 为会话设置的标志。

```console
gflags /i notepad.exe ffffffff 
```

作为响应，GFlags 会显示一条消息，指示没有为映像文件设置标志：

```console
No Registry Settings for notepad.exe executable 
```

 

 





