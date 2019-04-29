---
title: 调试双重引导计算机
description: 调试双重引导计算机
ms.assetid: 46ed532e-5ef3-4893-b2eb-da8eb52121f0
keywords:
- 双引导计算机
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9a503eb04f9af739fb0f53fedfa826820787745
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324593"
---
# <a name="debugging-a-dual-boot-machine"></a>调试双重引导计算机


## <span id="ddk_debugging_dual_boot_machines_dbg"></span><span id="DDK_DEBUGGING_DUAL_BOOT_MACHINES_DBG"></span>


您应该如何响应时备用操作系统不会启动双引导计算机上？

首先，检查启动选项指向其他操作系统的正确路径。 请参阅[获取设置以便进行调试](getting-set-up-for-debugging.md)有关详细信息。

在 x86 计算机，您还应该验证该 boosect.ini 存在。 此文件包含其他操作系统的启动记录。 若要取消隐藏此文件，请使用**attrib-r-s-h boosect.ini**命令。

 

 





