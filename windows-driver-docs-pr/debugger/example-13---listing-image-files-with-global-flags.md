---
title: 示例13列出带有全局标志的图像文件
description: 示例13列出带有全局标志的图像文件
ms.date: 10/12/2018
ms.localizationpriority: medium
ms.openlocfilehash: befaa8c7867373445d429c6ba9cd7b83c5072101
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792407"
---
# <a name="example-13-listing-image-files-with-global-flags"></a>示例13：列出包含全局标志的图像文件


## <span id="ddk_example_13___listing_image_files_with_global_flags_dtools"></span><span id="DDK_EXAMPLE_13___LISTING_IMAGE_FILES_WITH_GLOBAL_FLAGS_DTOOLS"></span>


GFlags 显示为特定图像文件设置的标志，但不显示具有标志集的所有图像文件。

Windows 在以下注册表路径中为映像文件（ **HKEY \_ 本地 \_ 计算机 \\ 软件 \\ Microsoft \\ Windows NT \\ CurrentVersion \\ 映像文件执行选项 \\ *ImageFileName* \\ GlobalFlag**）中的 **GlobalFlag** 注册表项存储文件的标志。

若要确定哪些映像文件设置了标志，请使用 Reg ( # A0) ，它是 Windows Server 2003 中包含的一种工具。

下面的 Reg **查询** 命令搜索指定注册表路径中的 **GlobalFlag** 注册表项。 **-V** 参数指定 **GlobalFlag** 注册表项。 **/S** 参数使得搜索是递归的。

```console
reg query "HKLM\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options" /v GlobalFlag /s
```

在响应中，Reg 显示路径中的 **GlobalFlag** 注册表项的所有实例以及该项的值。

```console
HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\notepad.exe
    GlobalFlag    REG_SZ    0x00001000

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\photohse.EXE
    GlobalFlag    REG_SZ    0x00200000

HKEY_LOCAL_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Image File Execution Options\printhse.EXE
    GlobalFlag    REG_SZ    0x00200000
```

**提示**   在记事本中键入 **Reg** 命令，然后将该文件保存为 imageflags.bat。 此后，若要查找已设置了标志的图像文件，只需键入 " **ImageFlags**"。

 

 

 





