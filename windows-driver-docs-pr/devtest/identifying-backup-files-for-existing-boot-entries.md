---
title: 识别现有启动项的备份文件
description: 识别现有启动项的备份文件
ms.assetid: 8f7e13b4-32f9-4b54-a8ab-db8148434ae8
keywords:
- NVRAM 启动选项 WDK，备份文件搜索
- EFI NVRAM 启动选项 WDK，备份文件搜索
- 搜索 WDK 启动选项
- 查找启动项备份 WDK
- 现有启动项搜索 WDK
- 启动项备份 WDK
- 标识启动项的备份文件
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: c65135498c65f9cf83dc19922f9bf8337968bf96
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384949"
---
# <a name="identifying-backup-files-for-existing-boot-entries"></a>识别现有启动项的备份文件

若要按文件名称搜索启动项的备份副本，需要提供条目的 EFI 启动项 ID。 但是，Bootcfg 和 Nvrboot 都不显示此 ID。

相反，你可以通过在 EFI 分区上的安装目录中搜索启动*xxxx* 文件来查找启动项备份副本。 若要查找安装目录，请找到操作系统安装的启动加载程序文件的路径。 安装的启动项备份文件存储在同一目录中。

使用 **nvrboot d** (显示) 命令或 **bootcfg** 或 **bootcfg 查询** 命令，以显示用于存储操作系统的启动加载程序的目录的路径。

在下面的示例中，启动项的启动加载程序存储在 \\ Microsoft WINNT50 子目录中的 EFI 分区上 \\ 。 此安装的启动条目的备份副本是同一子目录中名为 "启动*xxxx* " 的文件。

> [!NOTE]
> Bootcfg 中的 **启动项 ID** 字段和 Nvrboot 中的启动条目号不显示 EFI 启动项 id。 Bootcfg 和 Nvrboot Id 是表示启动 **条目** 部分中启动项顺序的行号，并在重新排序项时进行更改。

如下面的 Bootcfg 示例中所示，启动加载程序文件的路径显示在 **BootFilePath** 字段中。

Bootcfg 将文件位置显示为分区的 [NT 设备名称](../kernel/nt-device-names.md) ，后跟启动加载程序文件的文件系统路径。

```
Boot Entries
------------
Boot entry ID:    1
OS Friendly Name: Windows Server 2003, Enterprise
OsLoadOptions:     /debug /debugport=COM1 /baudrate=115200
BootFilePath:     \Device\HarddiskVolume1\EFI\Microsoft\WINNT50\ia64ldr.efi
OsFilePath:       \Device\HarddiskVolume3\WINDOWS
```

在 Nvrboot 显示的以下示例中，操作系统安装的启动加载器文件的路径显示在 " **EFIOSLoaderFilePath** " 字段中。

Nvrboot 将文件位置显示为分区 GUID，后跟启动加载程序文件的路径。

```
1. Load identifier = Windows Server 2003, Enterprise
2. OsLoadOptions = /debug /debugport=COM1 /baudrate=115209
3. EFIOSLoaderFilePath = 006F0073-0066-0074-5C00-570049004E00  ::  \EFI\Microsoft\WINNT50\ia64ldr.efi
4. OSLoaderFilePath = 04000004-5D18-3F27-0000-0000205C273F  :: \Windows
```

在这两种情况下，操作系统的启动加载器文件 (和启动*xxxx* 启动项备份文件) 都位于 efi 系统分区 (efi \\ Microsoft WINNT50) 的 WINNT50 目录中 \\ 。