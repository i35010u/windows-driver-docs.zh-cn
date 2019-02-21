---
title: GFlags 和 PageHeap
description: GFlags 和 PageHeap
ms.assetid: 9ced92d9-b37c-4db5-b3f9-fa2fe5325e57
keywords:
- GFlags、 GFlags 和 PageHeap
- PageHeap (pageheap.exe)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd97a2fdb94d1d9343ed3122655ff52d0bd7c4fc
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56521715"
---
# <a name="gflags-and-pageheap"></a>GFlags 和 PageHeap


## <span id="ddk_gflags_and_pageheap_dtools"></span><span id="DDK_GFLAGS_AND_PAGEHEAP_DTOOLS"></span>


此版本的 GFlags 包括 PageHeap (pageheap.exe)，一种工具，使监视在 Windows 中的堆分配的功能。 Pageheap 了启用 Windows 功能的保留的每个分配，以检测尝试访问超出分配的内存边界上的内存。

选择页面堆选项中 GFlags let*标准堆验证*，其中写入填充模式末尾的每个堆分配，并检查这些模式时已释放分配，或*整页堆验证*，这会无法访问页放在每次分配结束中该程序会立即停止如果访问超出分配的内存。 由于完整堆验证使用的每个分配的内存整页，其广泛的使用会导致系统内存短缺的状况。

-   若要启用的所有进程的标准页面堆验证，请使用**gflags /r + hpa**或**gflags /k + hpa**。

-   若要启用一个进程的标准页面堆验证，请使用**gflags/p /enable** *映像文件名*。

-   若要启用一个进程的整页堆验证，请使用**gflags /i** *映像文件名* **+ hpa**或者**gflags/p /enable** *映像文件名* **/full**。

所有页面堆设置除外 **/k**、 存储在注册表和保持有效，直到更改它们。

在解释小心**启用页堆**GFlags 对话框中的图像文件的复选框。 它指示页堆验证启用的图像文件，但它并不表示是否已满或标准页面堆验证。 如果检查结果从选中的复选框，然后完全为图像文件启用页堆验证。 但是，如果从命令行界面使用的检查结果，然后检查可以表示的图像文件是完全或标准页堆验证启用。

若要确定是否启用了完整或标准页堆验证程序，在命令行中，键入**gflags/p**。 在生成的显示中，**跟踪**指示标准页面堆验证已启用程序和**完整跟踪**指示为程序启用了整页堆验证。

 

 





