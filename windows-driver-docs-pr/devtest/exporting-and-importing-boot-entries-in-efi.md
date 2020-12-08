---
title: 导出和导入 EFI 中的启动项
description: 导出和导入 EFI 中的启动项
keywords:
- NVRAM 启动选项 WDK，导出
- EFI NVRAM 启动选项 WDK，导出
- NVRAM 启动选项 WDK，导入
- EFI NVRAM 启动选项 WDK，导入
- 导出启动条目 WDK
- 导入启动条目
- 启动项 Id WDK
- EFI 启动项 Id WDK
- 标识符 WDK 启动选项
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 072d8811d37221288f0c237bf21511ce27f25065
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804253"
---
# <a name="exporting-and-importing-boot-entries-in-efi"></a>导出和导入 EFI 中的启动项

使用 **nvrboot x** (export) 命令创建启动条目的备份副本。 设计命名和存储约定，以便在需要时轻松找到备份副本文件。

使用 **nvrboot i** (import) 命令从导出的备份副本导入或从安装程序创建的启动 *xxxx* 启动项备份文件中导入启动项。

导入的启动条目始终接收新的 EFI 启动项 Id。 例如，如果导出 Boot0003 的副本，然后将该副本导入到 NVRAM，则导入的启动项会收到新的启动项 ID，如 Boot000A。
