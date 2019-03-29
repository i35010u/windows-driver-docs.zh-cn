---
title: 识别已删除启动项的备份文件
description: 识别已删除启动项的备份文件
ms.assetid: ba1bcd10-83cb-4d28-9360-7927b169f056
keywords:
- NVRAM 启动选项 WDK，备份文件的搜索
- EFI NVRAM 启动选项 WDK，备份文件的搜索
- 搜索 WDK 启动选项
- 查找启动条目备份 WDK
- 删除启动条目搜索 WDK
- 启动条目备份 WDK
- 确定启动项的备份文件
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 728acc8c40ef4d3b71a53673ecb6f1d52994841a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566999"
---
# <a name="identifying-backup-files-for-deleted-boot-entries"></a>识别已删除启动项的备份文件

通常情况下，您需要查找启动入口备份文件时无意中删除的启动项。

如果 NVRAM，从已删除的启动项，仍安装操作系统的引导加载程序文件和安装的引导条目备份文件仍保留在磁盘上 EFI 分区上安装的目录中。

若要查找已删除的条目的启动项备份文件，启动到 EFI 外壳程序，并启动条目备份文件使用命令 EFI 分区以递归方式搜索**dir 引导\*/s**。 从结果中排除启动条目备份中的文件已在 NVRAM 中的启动项与相关联的目录。 若要显示现有的启动项目的目录，请使用**nvrboot d** （显示） 命令。

如果有多个启动*xxxx*不与现有的启动项相关联的文件使用 Nvrboot 从其备份文件导入项，然后删除不需要的启动项。
