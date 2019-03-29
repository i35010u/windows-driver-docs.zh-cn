---
title: 清单文件的位置
description: 清单文件的位置
ms.assetid: ebf10463-3aa1-403a-8508-1462259a5f8a
keywords:
- 日志查看器，清单，文件位置
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 802c9a859f59f703e5addf1d832c58a759bbd544
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563849"
---
# <a name="manifest-file-placement"></a>清单文件的位置


## <span id="ddk_manifest_file_placement_dtoolq"></span><span id="DDK_MANIFEST_FILE_PLACEMENT_DTOOLQ"></span>


主要的清单文件必须命名为 Main.h。

当运行时记录器时，Main.h 必须位于包含 Logexts.dll 的目录清单子目录中。

日志查看器是比记录器更灵活。 它将搜索 Main.h 按此顺序在以下目录：

1.  属于包含 Logviewer.exe 的目录清单的目录

2.  WinExt\\属于包含 logviewer.exe 的目录清单目录

3.  %Windir%\\System32\\清单目录

4.  %Windir%\\系统\\清单目录

所有附加清单文件必须位于与 Main.h 相同的目录。

 

 





