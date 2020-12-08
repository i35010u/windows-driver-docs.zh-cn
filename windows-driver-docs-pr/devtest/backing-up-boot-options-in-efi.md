---
title: 备份 EFI 中的启动选项
description: 备份 EFI 中的启动选项
keywords:
- 后退 ups WDK 启动选项，EFI
- NVRAM 启动选项 WDK，备份
- EFI NVRAM 启动选项 WDK，备份
- 正在复制启动选项
- 保存启动选项
- 启动选项 WDK，备份
- Nvrboot 工具
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6fb18ad228bb1aaa1c3cc1718e3caf3466f5dce9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784083"
---
# <a name="backing-up-boot-options-in-efi"></a>备份 EFI 中的启动选项


安装64位版本的 Windows 时，安装程序会自动创建一个用于安装的启动条目，并将启动项的备份副本保存到名为 "Boot *xxxx*" 的二进制文件中，其中 boot *xxxx* 是启动项的 NVRAM ID。 安装程序将启动项备份副本存储在 EFI 分区上的新目录中，以及用于新安装的 EFI 启动加载程序。默认情况下，安装目录位于 \\ EFI \\ Microsoft 子目录下 \\ 。

但是，系统不会保存你创建的启动条目的备份副本，并且不会在编辑后更新启动条目的备份副本。

若要保存你创建和编辑的启动条目的备份副本，并保存安装程序创建的条目的额外备份副本，请使用 Nvrboot (Nvrboot) 。 Nvrboot 以安装程序和 EFI 组件使用的二进制格式保存项。 然后，如果安装的启动条目丢失或损坏，则可以使用 Nvrboot 中 (**nvrboot i**) 中的 "导入" 命令将启动条目的备份副本导入到 NVRAM 中。

本节包括：

- [导出和导入 EFI 中的启动项](exporting-and-importing-boot-entries-in-efi.md)
- [识别现有启动项的备份文件](identifying-backup-files-for-existing-boot-entries.md)
- [识别已删除启动项的备份文件](identifying-backup-files-for-deleted-boot-entries.md)
- [识别不可用的启动项备份文件](recognizing-unusable-boot-entry-backup-files.md)
 





