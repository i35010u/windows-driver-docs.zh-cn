---
title: 关闭时删除
description: 关闭时删除
ms.assetid: 340e470f-7791-4677-9369-75ed8fa9f8ad
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 的文件系统，在关闭的删除
- FILE_DELETE_ON_CLOSE
- 关闭 WDK 的文件系统上的删除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9de3ae03f99ce02ed430250c73f66e3cfa4d388
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563202"
---
# <a name="delete-on-close"></a>关闭时删除


## <span id="ddk_delete_on_close_if"></span><span id="DDK_DELETE_ON_CLOSE_IF"></span>


当调用方指定了**文件\_删除\_ON\_关闭**选项，则很有必要的文件系统检查，以确保调用方对该文件具有删除权限或删除子级权限上父目录中。 任一权限就足以允许要删除的文件。 这是文件系统来处理重要情况。 按 I/O 管理器而是按文件系统，不会强制执行操作，在关闭时删除文件，其中的语义。

文件系统可能还需要检查卷没有写保护，此操作不适用于不允许此操作的目录。 例如，FASTFAT 文件系统代码执行受写保护的卷的检查，并且不允许删除使用文件的根目录\_删除\_ON\_关闭。 这些检查的示例可在**FatCommonCreate** Create.c 源文件从 WDK 包含 fastfat 示例中的函数。

 

 




