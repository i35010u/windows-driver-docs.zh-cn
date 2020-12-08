---
title: dbgerr002 指针错误
description: dbgerr002 指针错误
keywords:
- dbgerr002
- '错误的指针 (dbgerr002) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb3cf2e0dc0324eeee52358004548e0a91543916
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801983"
---
# <a name="dbgerr002-bad-pointer"></a>dbgerr002:错误的指针


## <span id="ddk_dbgerr002_dbg"></span><span id="DDK_DBGERR002_DBG"></span>


调试器错误 **dbgerr002** 显示消息 "指针错误"。 此错误表示检索符号文件时出现问题。

符号服务器已为该文件创建索引，但正在重定向到另一个位置以查找文件。 此位置没有可访问的文件。

此问题的两个常见原因是：

-   路径为 UNC 路径，但包含此服务器的计算机不可用。

-   路径指示已删除的目录或文件。

如果符号存储区是使用 SymStore 创建的，则可以通过检查文件 ptr 找到此文件的完整路径。 有关详细信息，请参阅 [使用 SymStore](symstore.md)。

 

 





