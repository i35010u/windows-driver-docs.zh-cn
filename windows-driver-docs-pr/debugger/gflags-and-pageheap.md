---
title: GFlags 和 PageHeap
description: GFlags 和 PageHeap
keywords:
- GFlags、GFlags 和 PageHeap
- 'PageHeap ( # A0) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14724b3860cbcd678595b2ccfb828e12bc79ad8a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838517"
---
# <a name="gflags-and-pageheap"></a>GFlags 和 PageHeap


## <span id="ddk_gflags_and_pageheap_dtools"></span><span id="DDK_GFLAGS_AND_PAGEHEAP_DTOOLS"></span>


此版本的 GFlags 包含 PageHeap ( # A0) 的功能，这是在 Windows 中启用堆分配监视的工具。 PageHeap 支持在每个分配的边界保留内存的 Windows 功能，以检测除分配之外的内存访问尝试。

通过 GFlags 中的页堆选项，您可以选择 *标准堆验证*，该验证在每个堆分配的末尾写入填充模式，并在释放分配时检查模式，或 *整页堆验证*，这会在每个分配的末尾放置不可访问的页，以便程序在访问超过分配的内存时立即停止。 由于完全堆验证对每个分配使用完整的内存页，因此它的广泛使用可能会导致系统内存不足。

-   若要对所有进程启用标准页堆验证，请使用 **gflags/r + hpa** 或 **gflags/k + hpa**。

-   若要为一个进程启用标准页堆验证，请使用 **gflags/p/Enable** *ImageFileName*。

-   若要为一个进程启用完整的页堆验证，请使用 **gflags/I** *ImageFileName* **+ hpa** 或 **gflags/p/enable** *ImageFileName* **/full**。

除 **/k** 之外的所有页面堆设置都存储在注册表中，并在您更改它们之前保持有效。

请注意，在 "GFlags" 对话框中解释图像文件的 " **启用页堆** " 复选框。 它表示为映像文件启用了页堆验证，但它并不表示它是完整的还是标准的页堆验证。 如果选中此复选框后的检查结果，则会为映像文件启用 "完全页堆验证"。 但是，如果通过使用命令行界面来检查结果，则该检查可以表示为映像文件启用完全或标准页堆验证。

若要确定是否为程序启用了完全或标准页堆验证，请在命令行中键入 **gflags/p**。 在生成的显示中，" **跟踪** " 指示为程序启用了标准页堆验证，而 " **完全跟踪** " 表示为该程序启用了 "完全页堆验证"。

 

 





