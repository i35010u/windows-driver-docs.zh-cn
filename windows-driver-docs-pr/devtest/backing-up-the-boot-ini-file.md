---
title: 备份 Boot.ini 文件
description: 在 Windows Vista 之前安装或升级基于 NT 的 Windows 操作系统时，Windows installer 将为该计算机创建新的 Boot.ini 文件。 新文件保留你可能对文件进行的部分（但不是全部）更改。
keywords:
- Boot.ini 文件 WDK，备份
- 后退 ups WDK 启动选项
- 恢复 ups WDK 启动选项，Boot.ini 文件
- 正在复制启动选项
- 保存启动选项
- 启动选项 WDK，备份
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 10eb8d89a3e3afa1055cda59b11aadaf16dfe7ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784081"
---
# <a name="backing-up-the-bootini-file"></a>备份 Boot.ini 文件


> [!IMPORTANT] 
> 本主题介绍 Windows XP 和 Windows Server 2003 中支持的启动选项。 如果要更改 Windows 的新式版本的启动选项，请参阅 [Windows (boot-options-in-windows.md) 中的 "启动选项"。

当你安装或升级到 Windows XP、Windows Server 2003 或其前一项时，Windows installer 将为计算机创建新的 *Boot.ini* 文件。 新文件保留你可能对文件进行的部分（但不是全部）更改。 因此，若要保留已编辑的 *Boot.ini* 文件，请在升级或安装操作系统之前创建备份副本。 更新完成后，可以将新文件替换为备份副本。 如果已安装新的操作系统，则可以从备份副本复制自定义的条目，然后将其粘贴到新的 *Boot.ini* 文件中。

更新或安装将还原 Boot.ini 上的默认安全属性，包括只读属性。 若要编辑该文件，请使用 Bootcfg 命令或更改文件属性。 有关详细信息，请参阅 [编辑 Boot.ini 文件](editing-the-boot-ini-file.md)。


