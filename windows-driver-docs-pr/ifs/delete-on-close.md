---
title: 关闭时删除
description: 关闭时删除
keywords:
- 安全 WDK 文件系统，语义模型检查
- 语义模型检查 WDK 文件系统，关闭时删除
- FILE_DELETE_ON_CLOSE
- 在关闭 WDK 文件系统时删除
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 972396585478460031169d3b3d7e88615fc34d83
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837271"
---
# <a name="delete-on-close"></a>关闭时删除


## <span id="ddk_delete_on_close_if"></span><span id="DDK_DELETE_ON_CLOSE_IF"></span>


如果调用方指定了 **" \_ \_ \_ 关闭时删除文件** " 选项，则文件系统检查是必需的，以确保调用方对该文件具有 delete 权限，或对父目录具有 delete 权限。 任何一个权限都足以允许删除文件。 这是文件系统处理的一个重要情况。 操作的语义（该操作在关闭时删除文件）不会由 i/o 管理器强制执行，而是由文件系统强制执行。

文件系统可能还需要检查卷是否未写入保护，此操作不会应用于不允许此操作的目录。 例如，FASTFAT 文件系统代码会检查是否存在写保护的卷，并且不允许 \_ 在关闭时使用文件删除删除根目录 \_ \_ 。 可在 WDK 包含的 fastfat 示例中的 **FatCommonCreate** 函数中找到这些检查的示例。

 

 




