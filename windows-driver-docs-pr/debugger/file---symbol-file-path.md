---
title: 文件符号文件路径
description: 文件符号文件路径
ms.assetid: 22d32b1b-d1b9-4627-99ed-08656da9b849
keywords:
- 文件符号文件路径
- 符号文件和路径，文件符号文件路径
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28f4b2a4a734841f084667a39c09f82863b7cdca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545928"
---
# <a name="file--symbol-file-path"></a>文件 |符号文件路径


## <span id="ddk_file_symbol_file_path_dbg"></span><span id="DDK_FILE_SYMBOL_FILE_PATH_DBG"></span>


单击**符号文件路径**上**文件**菜单显示、 设置，或将追加到符号路径。

此命令相当于按下 CTRL + S。

### <a name="span-idsymbolsearchpathdialogboxspanspan-idsymbolsearchpathdialogboxspansymbol-search-path-dialog-box"></a><span id="symbol_search_path_dialog_box"></span><span id="SYMBOL_SEARCH_PATH_DIALOG_BOX"></span>符号搜索路径对话框

当您单击**符号文件路径**，则**符号搜索路径**对话框随即出现。 此对话框显示当前符号路径。 如果**符号路径**框为空，则没有当前符号路径。

可以输入新路径，或编辑旧路径。 如果你想要搜索多个目录，请用分号分隔的目录名称。

单击**确定**以保存更改，或单击**取消**放弃更改。

如果选择**重新加载**复选框，调试器将重新加载所有已加载的符号和图像在单击后**确定**。 **重新加载**命令相当于使用[ **.reload （重新加载模块）** ](-reload--reload-module-.md)命令。

此外可以单击**浏览**以打开**浏览文件夹**对话框。

### <a name="span-idbrowseforfolderdialogboxspanspan-idbrowseforfolderdialogboxspanbrowse-for-folder-dialog-box"></a><span id="browse_for_folder_dialog_box"></span><span id="BROWSE_FOR_FOLDER_DIALOG_BOX"></span>浏览文件夹对话框

在中**浏览文件夹**对话框中，您可以浏览文件夹在您的计算机或网络上。 此外可以单击**建立新文件夹**按钮以创建新的文件夹。 如果您右键单击文件或文件夹在此对话框中，将显示标准 Windows 快捷方式菜单。

单击**确定**以将所选的文件夹附加到符号路径并返回到**符号搜索路径**对话框。

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关详细信息和更改的符号路径的其他方法，请参阅[符号路径](symbol-path.md)。

 

 





