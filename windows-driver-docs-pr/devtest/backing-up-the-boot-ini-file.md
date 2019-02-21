---
title: Boot.ini 文件备份
description: 当您安装或升级在 Windows Vista 之前基于 NT 的 Windows 操作系统时，Windows 安装程序将创建新计算机的 Boot.ini 文件。 新的文件保留部分，而不是全部，可能会对文件所做的更改。
ms.assetid: c4881f5d-3404-4e87-b130-33bc57b45ec9
keywords:
- Boot.ini 文件 WDK，备份
- 返回 ups WDK 启动选项
- 返回 ups WDK 启动选项，Boot.ini 文件
- 将复制启动选项
- 正在保存启动选项
- 启动选项 WDK，备份
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 467b034145356b8bd5ea429c1a9ac27f9f6ae2a1
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526382"
---
# <a name="backing-up-the-bootini-file"></a>Boot.ini 文件备份


> [!IMPORTANT] 
> 本主题介绍支持 Windows XP 和 Windows Server 2003 中的启动选项。 如果要更改的最新版本的 Windows 启动选项，请参阅[Windows Vista 和更高版本中的启动选项](boot-options-in-windows-vista-and-later.md)。

当你安装或升级到 Windows XP、 Windows Server 2003 或其中一个其前置任务时，Windows 安装程序创建一个新*Boot.ini*的计算机的文件。 新的文件保留部分，而不是全部，可能会对文件所做的更改。 因此，若要保留已编辑*Boot.ini*文件中，在升级或安装操作系统之前创建的备份副本。 更新完成后，可以将新文件替换为你的备份副本。 如果已安装新的操作系统，可以将自定义的项目备份副本从复制并粘贴到新*Boot.ini*文件。

更新或安装还原 Boot.ini，包括只读属性的默认安全属性。 若要编辑该文件，使用 Bootcfg 命令或更改文件属性。 有关详细信息，请参阅[编辑 Boot.ini 文件](editing-the-boot-ini-file.md)。


