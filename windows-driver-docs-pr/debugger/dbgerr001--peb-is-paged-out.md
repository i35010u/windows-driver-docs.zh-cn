---
title: dbgerr001 PEB 将分页输出
description: dbgerr001 PEB 将分页输出
ms.assetid: 60b20242-e458-4c36-b78d-17703c02b8b9
keywords:
- dbgerr001
- PEB 分页出 (dbgerr001)
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a81e0e2a6b8f2b4cf5892e88f989df9aa7527c7
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374935"
---
# <a name="dbgerr001-peb-is-paged-out"></a>dbgerr001:PEB 已移出页面


## <span id="ddk_dbgerr001_dbg"></span><span id="DDK_DBGERR001_DBG"></span>


调试器错误**dbgerr001**显示消息"PEB 调出中"。 此错误表示进程环境块 (PEB) 不可访问。

若要加载符号，调试器查看由操作系统加载模块的列表。 指向用户模式下的模块列表的指针是一个 PEB 中存储的项。

以回收内存，内存管理器可能会分页出用户模式下的数据，使空间用于其他进程或内核模式组件。

当发生此错误时，这意味着调试器已检测到此过程的 PEB 数据结构将无法阅读。 很可能是已分页输出到磁盘。

如果没有此数据结构，调试器无法确定哪些映像应为加载符号。

**请注意**  这只会影响用户模式模块的符号文件。 内核模式模块和符号不会影响，因为它们不同的列表中进行跟踪。

 

 

 





