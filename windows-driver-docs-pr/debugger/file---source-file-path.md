---
title: 文件源文件路径
description: 文件源文件路径
ms.assetid: 2fa7cbc1-a1e6-411b-95d2-18fd183ee117
keywords:
- 文件源文件路径
- 源文件和路径，文件源文件路径
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb8e079b111aecd4ebd3d99a27a8a90b2785e194
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252865"
---
# <a name="file--source-file-path"></a>文件 | 源文件路径


## <span id="ddk_file_source_file_path_dbg"></span><span id="DDK_FILE_SOURCE_FILE_PATH_DBG"></span>


选择 "**文件**" 菜单上的 "**源文件路径**" 以显示、设置或追加到源路径。

此命令等效于按 CTRL + P。

### <a name="span-idsource_search_path_dialog_boxspanspan-idsource_search_path_dialog_boxspansource-search-path-dialog-box"></a><span id="source_search_path_dialog_box"></span><span id="SOURCE_SEARCH_PATH_DIALOG_BOX"></span>"源搜索路径" 对话框

选择 " **源文件路径**" 时，将显示 " **源搜索路径** " 对话框。 此对话框显示当前源路径。 如果 " **源路径** " 框为空，则当前没有源路径。

您可以输入新路径或编辑旧路径。 如果要搜索多个目录，请用分号分隔目录名称。

如果要执行远程调试，则 **本地** 复选框将可用。 选择此框以编辑调试客户端的本地源路径;清除它可以编辑调试服务器的源路径。

选择 **"确定"** 以保存更改，或选择 " **取消** " 以放弃更改。

还可以选择 " **浏览** " 以打开 " **浏览文件夹** " 对话框。

### <a name="span-idbrowse_for_folder_dialog_boxspanspan-idbrowse_for_folder_dialog_boxspanbrowse-for-folder-dialog-box"></a><span id="browse_for_folder_dialog_box"></span><span id="BROWSE_FOR_FOLDER_DIALOG_BOX"></span>"浏览文件夹" 对话框

在 " **查找文件夹** " 对话框中，您可以浏览您的计算机或网络上的文件夹。 还可以选择 " **新建文件夹** " 按钮，创建一个新文件夹。 如果选择并按住 (右键单击此对话框中) 文件或文件夹，则会出现标准的 Windows 快捷菜单。

选择 **"确定"** 将所选文件夹追加到源路径，并返回到 " **源搜索路径** " 对话框。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息以及其他更改此路径的方法，请参阅 [源路径](source-path.md)。

 

 





