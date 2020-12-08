---
title: 调试双重引导计算机
description: 调试双重引导计算机
keywords:
- 双引导计算机
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e28546fcc123a414874e2dc0aba21e454f57d0e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813283"
---
# <a name="debugging-a-dual-boot-machine"></a>调试双重引导计算机


## <span id="ddk_debugging_dual_boot_machines_dbg"></span><span id="DDK_DEBUGGING_DUAL_BOOT_MACHINES_DBG"></span>


当备用操作系统未在双重引导计算机上启动时，应如何响应？

首先，检查启动选项是否指向其他操作系统的正确路径。 有关详细信息，请参阅 [获取调试设置](getting-set-up-for-debugging.md) 。

在 x86 计算机上，还应验证 boosect.ini 是否存在。 此文件包含其他操作系统的启动记录。 若要取消隐藏此文件，请使用 **attrib-r-s-h boosect.ini** 命令。

 

 





