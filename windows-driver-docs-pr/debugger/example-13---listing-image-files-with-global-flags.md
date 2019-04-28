---
title: 示例 13 列出与全局标志的图像文件
description: 示例 13 列出与全局标志的图像文件
ms.assetid: 1b1285d5-ed73-49c4-a123-de9cbdb3090c
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: 996f85db746fcc628ea6beb3de3b9249ee8e97bb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63347768"
---
# <a name="example-13-listing-image-files-with-global-flags"></a>示例 13：列出带有全局标志的映像文件


## <span id="ddk_example_13___listing_image_files_with_global_flags_dtools"></span><span id="DDK_EXAMPLE_13___LISTING_IMAGE_FILES_WITH_GLOBAL_FLAGS_DTOOLS"></span>


GFlags 显示对于特定的图像文件，设置的标志，但它不会显示已设置的标志的所有图像文件。

Windows 图像文件的存储标志**GlobalFlag**注册表项中的图像文件在以下注册表路径中，名为注册表子项**HKEY\_本地\_机\\软件\\Microsoft\\ Windows NT\\ CurrentVersion\\图像文件执行选项\\*映像文件名*\\GlobalFlag**。

若要确定哪个映像文件具有标志设置，请使用注册表 (reg.exe)，Windows Server 2003 中包含的工具。

以下 Reg**查询**命令搜索**GlobalFlag**中指定的注册表路径的注册表项。 **-V**参数指定**GlobalFlag**注册表项。 **/S**参数将使得搜索递归。

```console
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options" /v GlobalFlag /s
```

响应，显示的所有实例 Reg **GlobalFlag**注册表项中的路径和项的值。

```console
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\notepad.exe
    GlobalFlag    REG_SZ    0x00001000

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\photohse.EXE
    GlobalFlag    REG_SZ    0x00200000

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\printhse.EXE
    GlobalFlag    REG_SZ    0x00200000
```

**提示**  类型**Reg**命令到记事本中，然后将文件另存 imageflags.bat。 此后，若要查找已为其设置标志的图像文件，只需键入**ImageFlags**。

 

 

 





