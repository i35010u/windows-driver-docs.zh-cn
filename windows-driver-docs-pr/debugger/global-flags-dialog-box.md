---
title: 全局标志对话框
description: 全局标志对话框
keywords:
- GFlags，对话框
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 797004578a27f96271bada427267f35dede080a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834715"
---
# <a name="global-flags-dialog-box"></a>全局标志对话框


## <span id="ddk_global_flags_dialog_box_dtools"></span><span id="DDK_GLOBAL_FLAGS_DIALOG_BOX_DTOOLS"></span>


您可以使用 " **全局标志** " 对话框来设置和清除按名称列出所有标志的用户界面中的全局标志。 无需查找标志缩写或十六进制值。

此外，此对话框还提供对以下功能的访问，这些功能在命令行中不可用：

-   **调试器** −指定特定程序始终在调试器中运行。

-   **启动** −使用指定的调试设置运行程序。

-   **内核特殊池标记** −配置特殊池功能。

本主题包括以下过程的说明：

[打开对话框](opening-the-dialog-box.md)

[设置和清除系统范围的标志](setting-and-clearing-system-wide-flags.md)

[设置和清除内核标志](setting-and-clearing-kernel-flags.md)

[设置和清除映像文件标志](setting-and-clearing-image-file-flags.md)

[启动带标志的程序](launching-a-program-with-flags.md)

[在调试器中运行程序](running-a-program-in-a-debugger.md)

[配置特殊池](configuring-special-pool.md)

[配置对象引用跟踪](configuring-object-reference-tracing.md)

在 Windows Server 2003 和更高版本的 Windows 上永久启用池标记。 在这些系统中，"**全局标志**" 对话框中的 "**启用池标记**" 复选框将灰显，启用或禁用池标记的命令将失败。

请注意在 "**全局标志**" 对话框中对图像文件进行 "**启用页堆**" 复选框。 此复选框指示为映像文件启用了页面堆验证，但它并不表明它是完整的还是标准的页堆验证。 如果选中此复选框后的检查结果，则会为映像文件启用 "完全页堆验证"。 但是，如果通过使用命令行界面来检查结果，则该检查可以表示为映像文件启用完全或标准页堆验证。

若要确定是否为程序启用了完全或标准页堆验证，请在命令行中键入 **gflags/p**。 在生成的显示中，" **跟踪** " 指示为程序启用了标准页堆验证，而 " **完全跟踪** " 表示为该程序启用了 "完全页堆验证"。

 

 





