---
title: 文件符号文件路径
description: 文件符号文件路径
keywords:
- 文件符号文件路径
- 符号文件和路径，文件符号文件路径
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab856c1ebae5f20a2237730a0efe9b8995c9b052
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838207"
---
# <a name="file--symbol-file-path"></a>文件 | 符号文件路径


## <span id="ddk_file_symbol_file_path_dbg"></span><span id="DDK_FILE_SYMBOL_FILE_PATH_DBG"></span>


单击 "**文件**" 菜单上的 "**符号文件路径**"，以显示、设置或追加到符号路径。

此命令等效于按 CTRL + S。

### <a name="span-idsymbol_search_path_dialog_boxspanspan-idsymbol_search_path_dialog_boxspansymbol-search-path-dialog-box"></a><span id="symbol_search_path_dialog_box"></span><span id="SYMBOL_SEARCH_PATH_DIALOG_BOX"></span>"符号搜索路径" 对话框

单击 " **符号文件路径**" 时，将显示 " **符号搜索路径** " 对话框。 此对话框显示当前符号路径。 如果 " **符号路径** " 框为空，则没有当前符号路径。

您可以输入新路径或编辑旧路径。 如果要搜索多个目录，请用分号分隔目录名称。

单击 **"确定"** 以保存更改，或单击 " **取消** " 以放弃更改。

如果选中 " **重新加载** " 复选框，则调试器将在您单击 **"确定"** 后重新加载所有加载的符号和图像。 **重载** 命令等效于使用 [**. Reload.sql (reload.sql Module)**](-reload--reload-module-.md)命令。

还可以单击 " **浏览** " 打开 " **浏览文件夹** " 对话框。

### <a name="span-idbrowse_for_folder_dialog_boxspanspan-idbrowse_for_folder_dialog_boxspanbrowse-for-folder-dialog-box"></a><span id="browse_for_folder_dialog_box"></span><span id="BROWSE_FOR_FOLDER_DIALOG_BOX"></span>"浏览文件夹" 对话框

在 " **查找文件夹** " 对话框中，您可以浏览您的计算机或网络上的文件夹。 还可以单击 " **新建文件夹** " 按钮创建一个新文件夹。 如果右键单击此对话框中的某个文件或文件夹，则会出现标准的 Windows 快捷菜单。

单击 **"确定"** 将所选文件夹追加到符号路径中，并返回到 " **符号搜索路径** " 对话框。

### <a name="span-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息以及其他更改符号路径的方法，请参阅 [符号路径](symbol-path.md)。

 

 





