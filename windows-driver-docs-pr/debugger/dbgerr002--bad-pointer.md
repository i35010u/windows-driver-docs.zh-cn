---
title: dbgerr002 无效的指针
description: dbgerr002 无效的指针
ms.assetid: d5f2404e-3e7d-4de2-a772-0d42169eb9ad
keywords:
- dbgerr002
- 无效的指针 (dbgerr002)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 97c0a79de5df862985213bb4c378fd011f8e917f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373452"
---
# <a name="dbgerr002-bad-pointer"></a>dbgerr002:错误的指针


## <span id="ddk_dbgerr002_dbg"></span><span id="DDK_DBGERR002_DBG"></span>


调试器错误**dbgerr002**显示消息"错误的指针。" 此错误表示检索的符号文件的问题。

符号服务器已编制索引，该文件，但已被重定向到其他位置，以查找该文件。 在此其他位置，没有文件进行访问。

此问题的两个常见原因是：

-   路径是 UNC 路径，并包含此服务器的计算机不可用。

-   该路径表示目录或文件已被删除。

如果创建使用 SymStore 符号存储区，您可以通过检查 file.ptr 找到此文件的完整路径。 有关详细信息，请参阅[使用 SymStore](symstore.md)。

 

 





