---
title: dbgerr004 转储文件中页不存在
description: dbgerr004 转储文件中页不存在
ms.assetid: e76d11fc-857b-4a40-8f41-f34f3bcade57
keywords:
- dbgerr004
- 转储文件 (dbgerr004) 中不存在页
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91602c01f37f74844e263b7457f29b8aff6e442c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63374387"
---
# <a name="dbgerr004-page-not-present-in-dump-file"></a>dbgerr004:转储文件中不存在页面


## <span id="ddk_dbgerr004_dbg"></span><span id="DDK_DBGERR004_DBG"></span>


调试器错误**dbgerr004**将显示消息"页*数*转储文件中不存在。" 此错误指示调试器需要未包含在调试转储文件中的内存页面。

指定*数*是页帧数 (PFN) 对应于原始页面的物理内存中的位置。

若要禁止显示此错误消息，请使用[ **.ignore\_缺少\_页 1** ](-ignore-missing-pages--suppress-missing-page-errors-.md)命令。 此命令允许调试若要继续，但不显示此错误消息。

内核模式内存转储有三种大小和较小的大小不包括所有的内存页面。 有关详细信息，请参阅[种内核模式转储文件的](varieties-of-kernel-mode-dump-files.md)。

用户模式内存转储也有各种大小。 请参阅[用户模式转储文件](user-mode-dump-files.md)有关详细信息。

 

 





