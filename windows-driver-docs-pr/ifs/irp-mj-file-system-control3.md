---
title: IRP_MJ_FILE_SYSTEM_CONTROL
description: IRP_MJ_FILE_SYSTEM_CONTROL
ms.assetid: 38b88379-c007-4e88-a6d9-5aacd6bdefd3
keywords:
- IRP_MJ_FILE_SYSTEM_CONTROL
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 的文件系统，IRP_MJ_FILE_SYSTEM_CONTROL
- 文件系统控件 WDK 安全性
- 设置处理 WDK 文件系统的文件信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67c1808a9aa5c250814b7aea834acd0c48df8e13
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565066"
---
# <a name="irpmjfilesystemcontrol"></a>IRP_MJ_FILE_SYSTEM_CONTROL


文件系统控制允许文件系统，从而执行实质上是任何特殊的操作。 现有 Windows 文件系统都有许多的专用控件，并且它们，以及针对 Windows 开发的任何第三方文件系统，则必须积极地检查所有参数。 此外，FSCTL 操作通常具有受限的安全权限。 这些可以在 WDK 包含 FASTFAT 示例代码所示 (请参阅**FatInvalidateVolumes**中 fsctrl.c，例如函数)。 这是特权检查的示例。 在这种情况下 FASTFAT 文件系统的策略是需要给定的权限在系统上启用。

如果文件系统已在使用 CTL_CODE 宏的文件系统操作定义中设置这些位，I/O 管理器将强制执行针对特定的 FSCTL 操作 FILE_READ_DATA 和 FILE_WRITE_DATA 权限。 必须检查所需的所有其他权限通过文件系统 （例如 FILE_READ_ATTRIBUTES 权限） 如果这是文件系统的策略。

 

 




