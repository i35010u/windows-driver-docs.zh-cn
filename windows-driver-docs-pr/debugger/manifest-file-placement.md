---
title: 清单文件的位置
description: 清单文件的位置
keywords:
- LogViewer、清单、文件放置
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3b1380f087f92a0c3e8b2cb5fcb3f481029f8693
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814565"
---
# <a name="manifest-file-placement"></a>清单文件的位置


## <span id="ddk_manifest_file_placement_dtoolq"></span><span id="DDK_MANIFEST_FILE_PLACEMENT_DTOOLQ"></span>


主清单文件必须命名为 Main。

当记录器正在运行时，Main .h 必须位于包含 Logexts.dll 的目录的清单子目录中。

LogViewer 比记录器更灵活。 它将按以下顺序在以下目录中搜索 Main .h：

1.  从属于包含 Logviewer.exe 的目录的清单目录

2.  \\包含 logviewer.exe 的目录的从属 WinExt 清单目录

3.  % WinDir% \\ System32 \\ 清单目录

4.  % WinDir% \\ 系统 \\ 清单目录

所有其他清单文件必须位于与 Main .h 相同的目录中。

 

 





