---
title: 转储文件中不存在 dbgerr004 页面
description: 转储文件中不存在 dbgerr004 页面
keywords:
- dbgerr004
- '页面在转储文件中不存在 (dbgerr004) '
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 53247c75df84211c50e7d4cdd567e48545bb15f3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831599"
---
# <a name="dbgerr004-page-not-present-in-dump-file"></a>dbgerr004:转储文件中不存在页面


## <span id="ddk_dbgerr004_dbg"></span><span id="DDK_DBGERR004_DBG"></span>


调试器错误 **dbgerr004** 显示消息 "页面 *编号* 在转储文件中不存在。" 此错误表示调试器需要的内存页未包含在正在调试的转储文件中。

指定的 *数字* 是页面框架编号 (PFN) 对应于原始页面的物理内存中的位置。

若要取消显示此错误消息，请使用 " [**忽略 \_ 缺少的 \_ 页 1**](-ignore-missing-pages--suppress-missing-page-errors-.md) " 命令。 此命令允许进行调试，但不显示此错误消息。

内核模式内存转储为三种大小，较小的大小不包括所有内存页。 有关详细信息，请参阅 [多种 Kernel-Mode 转储文件](varieties-of-kernel-mode-dump-files.md)。

用户模式内存转储也有各种大小。 有关详细信息，请参阅 [用户模式转储文件](user-mode-dump-files.md) 。

 

 





