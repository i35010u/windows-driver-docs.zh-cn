---
title: 备份 EFI 中的启动选项
description: 备份 EFI 中的启动选项
ms.assetid: a9c7052c-c554-460c-a8ba-12b79126e67f
keywords:
- 返回 ups WDK 启动选项，EFI
- NVRAM 启动选项 WDK，备份
- EFI NVRAM 启动选项 WDK，备份
- 将复制启动选项
- 正在保存启动选项
- 启动选项 WDK，备份
- Nvrboot 工具
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: a72f7b449c7bc42ec938077c76467070d90737ca
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576018"
---
# <a name="backing-up-boot-options-in-efi"></a>备份 EFI 中的启动选项


在安装 Windows 的 64 位版本时，安装程序自动创建安装的启动项并将启动项目的备份副本保存到名为启动的二进制文件*xxxx*，其中引导*xxxx*是启动项目的的 NVRAM ID。 安装程序将启动条目备份副本存储在 EFI 分区，以及用于新安装 EFI 启动加载程序上的新目录。默认情况下，安装目录位于\\EFI\\Microsoft\\子目录。

但是，系统不会保存您创建的启动项的备份副本，并且它不会更新的启动项的备份副本之后你对其进行编辑。

若要保存备份副本的启动项的创建和编辑，并保存安装程序创建的条目的额外备份副本，请使用 Nvrboot (nvrboot.efi)。 Nvrboot 将保存安装程序和 EFI 组件使用的二进制格式中的条目。 然后，如果安装了启动项目已丢失或已损坏，您可以使用导入命令 (**nvrboot 我**) Nvrboot 导入到 NVRAM 的启动项目的备份副本中。

本部分包括：

- [导出和导入在 EFI 启动项](exporting-and-importing-boot-entries-in-efi.md)
- [识别备份文件的现有启动项](identifying-backup-files-for-existing-boot-entries.md)
- [识别备份文件已删除的启动项](identifying-backup-files-for-deleted-boot-entries.md)
- [识别不可用的启动项的备份文件](recognizing-unusable-boot-entry-backup-files.md)
 





