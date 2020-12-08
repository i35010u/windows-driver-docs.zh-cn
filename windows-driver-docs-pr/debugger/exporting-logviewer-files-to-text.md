---
title: 将 LogViewer 文件导出为文本
description: 将 LogViewer 文件导出为文本
keywords:
- LogViewer，将文件导出到文本
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73bb9a1d573af1aa719a01162eb2641a609885a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838217"
---
# <a name="exporting-logviewer-files-to-text"></a>将 LogViewer 文件导出为文本


## <span id="ddk_exporting_logviewer_files_to_text_dtoolq"></span><span id="DDK_EXPORTING_LOGVIEWER_FILES_TO_TEXT_DTOOLQ"></span>


操作日志文件的一种有效方法是将其导出到文本。 这允许您使用 "查找" 功能的任何文本编辑器来查找特定的参数值。 尽管可以直接通过记录器生成文本文件，但如果使用 LogViewer 筛选函数调用或添加别名，然后将此信息导出到文本文件中，则会有更多的灵活性。

若要从 lgv 文件创建文本文件，请在 LogViewer 中打开该文件，然后选择 " **文件" | "导出到文本**。 在对话框中，选择文件名和位置。

对话框底部有几个选项：

<span id="Export_Diff_Information"></span><span id="export_diff_information"></span><span id="EXPORT_DIFF_INFORMATION"></span>**导出差异信息**  
此选项会将所有指针、句柄值和其他从执行更改为执行的值作为别名。 不会输出指针的实际值 (例如，"0x00123FA2" ) ，LogViewer 将输出 "指针"。 同样，句柄将化名为 "HeapHandle1" 或一些其他值，当使用差异工具比较两个文件时，这些值将不作为 *差异* 进行注册。

<span id="Include_Non-Visible_Rows"></span><span id="include_non-visible_rows"></span><span id="INCLUDE_NON-VISIBLE_ROWS"></span>**包含不可见的行**  
此选项将禁用导出时当前应用于视图的任何筛选器。

<span id="Create_a_Separate_File_For_Each_Thread"></span><span id="create_a_separate_file_for_each_thread"></span><span id="CREATE_A_SEPARATE_FILE_FOR_EACH_THREAD"></span>**为每个线程创建一个单独的文件**  
此选项按线程拆分文本文件，使执行线程更容易。 如果打算 "差异" 两个执行实例，这会很有用。

<span id="Export_Range"></span><span id="export_range"></span><span id="EXPORT_RANGE"></span>**导出范围**  
此选项指定要导出的行范围。

 

 





