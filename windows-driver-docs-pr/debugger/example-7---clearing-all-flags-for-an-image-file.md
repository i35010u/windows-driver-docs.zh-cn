---
title: 示例 7 清除所有标志的图像文件
description: 示例 7 清除所有标志的图像文件
ms.assetid: 832c79de-07ca-4212-b3b3-ace396986ebb
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 079f2b24110e1d0116a998d2af87c57d944e5173
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562497"
---
# <a name="example-7-clearing-all-flags-for-an-image-file"></a>示例 7：清除映像文件的所有标志


## <span id="ddk_example_7___clearing_all_flags_for_an_image_file_dtools"></span><span id="DDK_EXAMPLE_7___CLEARING_ALL_FLAGS_FOR_AN_IMAGE_FILE_DTOOLS"></span>


以下命令将清除所有标志和图像的图像文件的调试器选项。 该命令将高值 (0xFFFFFFFF) 添加到当前的标志值。 通过删除响应 GFlags **GlobalFlag**图像文件，从而删除的所有值将存储在注册表项。

此命令不会影响整个系统中设置标志**GlobalFlag**注册表项或标志设置为会话 （内核模式）。

```console
gflags /i notepad.exe ffffffff 
```

在响应中，用 GFlags 显示一个消息指示没有标志设置为图像文件：

```console
No Registry Settings for notepad.exe executable 
```

 

 





