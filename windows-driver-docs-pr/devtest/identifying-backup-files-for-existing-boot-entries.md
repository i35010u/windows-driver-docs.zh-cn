---
title: 识别现有启动项的备份文件
description: 识别现有启动项的备份文件
ms.assetid: 8f7e13b4-32f9-4b54-a8ab-db8148434ae8
keywords:
- NVRAM 启动选项 WDK，备份文件的搜索
- EFI NVRAM 启动选项 WDK，备份文件的搜索
- 搜索 WDK 启动选项
- 查找启动条目备份 WDK
- 现有的启动项搜索 WDK
- 启动条目备份 WDK
- 确定启动项的备份文件
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 8777a62ce485103921a1c7bc93ce160be870d580
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56565455"
---
# <a name="identifying-backup-files-for-existing-boot-entries"></a>识别现有启动项的备份文件

若要按其文件名称搜索的启动项的备份副本，你需要条目的 EFI 启动项目 id。 但是，Bootcfg 和 Nvrboot 都不显示此 id。

相反，可以通过启动搜索找到启动条目备份副本*xxxx* EFI 分区上安装的目录中的文件。 若要查找的安装目录，找到操作系统安装启动加载程序文件的路径。 启动项安装的备份文件存储在相同的目录。

使用**nvrboot d** （显示） 命令或**bootcfg**或**bootcfg 查询**命令以显示操作系统的启动加载器所在的目录的路径存储中。

在以下示例中，为启动项目的启动加载器存储中的 EFI 分区上\\Microsoft\\WINNT50 子目录。 此安装的启动项目的备份副本是一个名为启动文件*xxxx*同一子目录中。

> [!NOTE]
> **启动项目 ID** Bootcfg 中的字段和启动 Nvrboot 中的项数不显示 EFI 启动项目 id。 Bootcfg 和 Nvrboot Id 所表示的启动项目中的顺序的行号**启动项**部分，并更改时重新排序项。

当以下 Bootcfg 示例中所示，引导加载程序文件的路径将显示在**BootFilePath**字段。

Bootcfg 显示为的文件位置[NT 设备名称](https://docs.microsoft.com/windows-hardware/drivers/kernel/nt-device-names)跟启动加载程序文件的文件系统路径的分区。

```
Boot Entries
------------
Boot entry ID:    1
OS Friendly Name: Windows Server 2003, Enterprise
OsLoadOptions:     /debug /debugport=COM1 /baudrate=115200
BootFilePath:     \Device\HarddiskVolume1\EFI\Microsoft\WINNT50\ia64ldr.efi
OsFilePath:       \Device\HarddiskVolume3\WINDOWS
```

在下面的示例 Nvrboot 显示操作系统安装启动加载程序文件的路径显示在**EFIOSLoaderFilePath**字段。

Nvrboot 作为分区 GUID 其后的引导加载程序文件路径显示的文件位置。

```
1. Load identifier = Windows Server 2003, Enterprise
2. OsLoadOptions = /debug /debugport=COM1 /baudrate=115209
3. EFIOSLoaderFilePath = 006F0073-0066-0074-5C00-570049004E00  ::  \EFI\Microsoft\WINNT50\ia64ldr.efi
4. OSLoaderFilePath = 04000004-5D18-3F27-0000-0000205C273F  :: \Windows
```

在这两种情况下，启动加载程序文件 (和启动*xxxx*启动入口备份文件) 的操作系统是 EFI 系统分区的 WINNT50 目录中 (EFI\\Microsoft\\WINNT50)。
