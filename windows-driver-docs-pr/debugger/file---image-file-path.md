---
title: 文件图像文件路径
description: 文件图像文件路径
keywords:
- 文件图像文件路径
- 可执行文件和路径，文件图像文件路径
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fc9cd89aebeea7474f1c541fd2cb6da6bee9e1d5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833665"
---
# <a name="file--image-file-path"></a>文件 | 映像文件路径


## <span id="ddk_file_image_file_path_dbg"></span><span id="DDK_FILE_IMAGE_FILE_PATH_DBG"></span>


选择 "**文件**" 菜单上的 "**图像文件路径**"，以显示、设置或追加到可执行映像路径。

此命令等效于按 CTRL + I。

### <a name="span-idexecutable_image_search_path_dialog_boxspanspan-idexecutable_image_search_path_dialog_boxspanexecutable-image-search-path-dialog-box"></a><span id="executable_image_search_path_dialog_box"></span><span id="EXECUTABLE_IMAGE_SEARCH_PATH_DIALOG_BOX"></span>"可执行图像搜索路径" 对话框

当您选择 " **图像文件路径**" 时，将出现 " **可执行文件图像搜索路径** " 对话框。 此对话框显示当前的可执行映像路径。 如果 " **图像路径** " 框为空，则当前没有可执行的映像路径。

您可以输入新路径或编辑旧路径。 如果要搜索多个目录，请用分号分隔目录名称。

选择 **"确定"** 以保存更改，或选择 " **取消** " 以放弃更改。

如果选中 " **重新加载** " 复选框，则调试器将在您选择 **"确定"** 后重新加载所有加载的图像和符号文件。 此命令等效于使用 [**. reload.sql (Reload.sql Module)**](-reload--reload-module-.md) 命令。

还可以选择 " **浏览** " 以打开 " **浏览文件夹** " 对话框。

### <a name="span-idbrowse_for_folder_dialog_boxspanspan-idbrowse_for_folder_dialog_boxspanbrowse-for-folder-dialog-box"></a><span id="browse_for_folder_dialog_box"></span><span id="BROWSE_FOR_FOLDER_DIALOG_BOX"></span>"浏览文件夹" 对话框

在 " **查找文件夹** " 对话框中，您可以浏览您的计算机或网络上的文件夹。 你还可以使用 " **新建文件夹** " 按钮创建一个新文件夹。 如果在此对话框中选择并按住 (或右键单击) 文件或文件夹，则会出现标准的 Windows 快捷菜单。

选择 **"确定"** 将所选文件夹追加到可执行映像路径，并返回到 " **可执行图像搜索路径** " 对话框。

 

 





