---
title: dbgerr001 PEB 已分页
description: dbgerr001 PEB 已分页
keywords:
- dbgerr001
- PEB)  (dbgerr001
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5bb0a1ba288193ca66c619117d6320630d41de06
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788833"
---
# <a name="dbgerr001-peb-is-paged-out"></a>dbgerr001:PEB 已移出页面


## <span id="ddk_dbgerr001_dbg"></span><span id="DDK_DBGERR001_DBG"></span>


调试器错误 **dbgerr001** 显示消息 "PEB 已分页出"。 此错误表示进程环境块 (PEB) 不可访问。

若要加载符号，调试器会查看操作系统加载的模块的列表。 指向用户模式模块列表的指针是 PEB 中存储的项之一。

为了回收内存，内存管理器可能会分页输出用户模式数据，为其他进程或内核模式组件腾出空间。

发生此错误时，表示调试器已检测到此进程的 PEB 数据结构不再可读。 最可能的是，已被分页到磁盘。

如果没有此数据结构，调试器将无法确定应该为哪些图像加载符号。

**注意**   这只会影响用户模式模块的符号文件。 内核模式模块和符号不受影响，因为它们是在其他列表中跟踪的。

 

 

 





