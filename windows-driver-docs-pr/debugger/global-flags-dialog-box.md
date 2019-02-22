---
title: 全局标志对话框
description: 全局标志对话框
ms.assetid: c6987d72-4141-45f2-af06-f4c7040a7e6b
keywords:
- GFlags、 对话框
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a3d514d8ac487435b4202eb8753b0e6caa3a167c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521395"
---
# <a name="global-flags-dialog-box"></a>全局标志对话框


## <span id="ddk_global_flags_dialog_box_dtools"></span><span id="DDK_GLOBAL_FLAGS_DIALOG_BOX_DTOOLS"></span>


可以使用**全局标志**对话框中设置和清除与按名称列出所有标志的用户界面中的全局标志。 没有无需查找标志缩写或十六进制值。

此外，对话框中提供了访问命令行中不可用的以下功能：

-   **调试器**− 指定特定程序始终在调试器中运行。

-   **启动**− 使用指定的调试设置运行的程序。

-   **内核特殊池标记**− 配置特殊池功能。

本主题包含有关以下过程的说明：

[打开对话框的](opening-the-dialog-box.md)

[设置和清除整个系统标志](setting-and-clearing-system-wide-flags.md)

[设置和清除内核标志](setting-and-clearing-kernel-flags.md)

[设置和清除图像文件标志](setting-and-clearing-image-file-flags.md)

[启动具有标志的程序](launching-a-program-with-flags.md)

[在调试器中运行的程序](running-a-program-in-a-debugger.md)

[配置特殊的池](configuring-special-pool.md)

[配置对象引用跟踪](configuring-object-reference-tracing.md)

Windows Server 2003 和更高版本的 Windows 上永久启用池标记。 在这些系统上**启用池标记**上的复选框**全局标志**对话框灰显，并且命令来启用或禁用池标记失败。

在解释小心**启用页堆**中的图像文件的复选框**全局标志**对话框。 此复选框指示页堆验证启用的图像文件，但它并不表示是否已满或标准页面堆验证。 如果检查结果从选中的复选框，然后完全为图像文件启用页堆验证。 但是，如果从命令行界面使用的检查结果，然后检查可以表示的图像文件是完全或标准页堆验证启用。

若要确定是否启用了完整或标准页面堆验证程序，在命令行中，键入**gflags/p**。 在生成的显示中，**跟踪**指示标准页面堆验证已启用程序和**完整跟踪**指示为程序启用了整页堆验证。

 

 





