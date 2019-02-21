---
title: 导出到文本日志查看器文件
description: 导出到文本日志查看器文件
ms.assetid: b014dc23-ca6e-4563-aa8d-f4dd19c89f80
keywords:
- 日志查看器，将文件导出到文本
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: fab8c7e2d24af8c73434d25cc3802995f6bbfa54
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541380"
---
# <a name="exporting-logviewer-files-to-text"></a>导出到文本日志查看器文件


## <span id="ddk_exporting_logviewer_files_to_text_dtoolq"></span><span id="DDK_EXPORTING_LOGVIEWER_FILES_TO_TEXT_DTOOLQ"></span>


操作日志文件的有效方式是将它们导出为文本。 这可以通过使用任何文本编辑器的查找功能查找特定的参数值。 虽然可以为要由记录器直接生成的文本文件，但如果使用日志查看器来筛选函数调用或添加别名，，然后将导出到文本文件此信息将具有更大的灵活性。

若要从.lgv 文件创建一个文本文件，在日志查看器，打开文件，然后选择**文件 |将导出到文本**。 在对话框中，选择文件名和位置。

有几个选项在对话框的底部：

<span id="Export_Diff_Information"></span><span id="export_diff_information"></span><span id="EXPORT_DIFF_INFORMATION"></span>**导出差异的信息**  
此选项会将别名，所有指针、 句柄值和更改执行执行的其他值。 日志查看器将不需要输出指针 (例如，"0x00123FA2") 的实际值，输出"指针"。 同样，句柄将作为使用别名"HeapHandle1"或无法将注册为其他值*差异*时使用差异比较工具比较两个文件。

<span id="Include_Non-Visible_Rows"></span><span id="include_non-visible_rows"></span><span id="INCLUDE_NON-VISIBLE_ROWS"></span>**包含不可见的行**  
此选项将禁用任何筛选器当前应用于导出时的视图。

<span id="Create_a_Separate_File_For_Each_Thread"></span><span id="create_a_separate_file_for_each_thread"></span><span id="CREATE_A_SEPARATE_FILE_FOR_EACH_THREAD"></span>**为每个线程创建一个单独的文件**  
此选项将该文本文件拆分由线程，使其易于进行跟踪的执行线程。 这是你想将到"diff"执行的两个实例的情况下很有用。

<span id="Export_Range"></span><span id="export_range"></span><span id="EXPORT_RANGE"></span>**导出范围**  
此选项指定要导出的行的范围。

 

 





