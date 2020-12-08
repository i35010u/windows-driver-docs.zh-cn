---
title: 识别已删除启动项的备份文件
description: 识别已删除启动项的备份文件
keywords:
- NVRAM 启动选项 WDK，备份文件搜索
- EFI NVRAM 启动选项 WDK，备份文件搜索
- 搜索 WDK 启动选项
- 查找启动项备份 WDK
- 已删除启动项搜索 WDK
- 启动项备份 WDK
- 标识启动项的备份文件
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: ef5b4aaab858bd74ac4cc5a9a3f019b46efc7887
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824639"
---
# <a name="identifying-backup-files-for-deleted-boot-entries"></a>识别已删除启动项的备份文件

通常，在无意中删除启动项时，需要查找启动项备份文件。

如果已从 NVRAM 中删除启动项，并且仍在安装操作系统，则启动加载程序文件和安装的启动项备份文件仍保留在 EFI 分区上安装目录中的磁盘上。

若要查找已删除条目的启动项目备份文件，请启动到 EFI shell，并使用命令 **目录 boot \* /s** 以递归方式搜索 efi 分区以进行启动项备份文件。 从结果启动条目备份文件中排除，这些文件位于与 NVRAM 中已有的启动条目关联的目录中。 若要显示现有启动项的目录，请使用 **nvrboot d** (显示) "命令。

如果有多个启动 *xxxx* 文件不与现有启动条目关联，请使用 Nvrboot 从其备份文件中导入条目，然后删除不需要的启动条目。
