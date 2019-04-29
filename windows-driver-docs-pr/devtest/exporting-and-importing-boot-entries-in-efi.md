---
title: 导出和导入 EFI 中的启动项
description: 导出和导入 EFI 中的启动项
ms.assetid: bd019064-cb8c-434c-b471-192168564540
keywords:
- NVRAM 启动选项 WDK，导出
- EFI NVRAM 启动选项 WDK，导出
- NVRAM 启动选项 WDK，导入
- EFI NVRAM 启动选项 WDK，导入
- 导出 WDK 的启动项目
- 导入启动项
- 启动项目 Id WDK
- EFI 启动项 Id WDK
- 标识符 WDK 启动选项
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: d0f19d6219aa1c1fdf057ad2884b71f75ef3f508
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378813"
---
# <a name="exporting-and-importing-boot-entries-in-efi"></a>导出和导入 EFI 中的启动项

使用**nvrboot x** （导出） 命令，以创建一份备份的启动项。 设计可轻松在需要时查找的备份副本文件命名和存储约定。

使用**nvrboot 我**（导入） 命令以从导出的备份副本或启动导入启动条目*xxxx*启动安装程序创建的项的备份文件。

导入的启动项一定会收到新的 EFI 启动项 Id。 例如，如果导出 Boot0003，一份，然后将该副本导入 NVRAM 导入的启动项收到新的启动项目 ID，如 Boot000A。
