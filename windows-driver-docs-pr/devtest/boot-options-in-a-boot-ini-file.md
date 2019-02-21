---
title: Boot.ini 文件中的启动选项
description: Boot.ini 是系统分区，通常 c:\Boot.ini 根处的文本文件。 Boot.ini 存储启动传统上，具有 x86 和基于 x64 的处理器的计算机具有 BIOS 固件的计算机的选项。
ms.assetid: a2593b6d-03df-49d1-ae77-efec4c2ac8be
keywords:
- Boot.ini 文件 WDK
- 启动 WDK，Boot.ini 文件选项
ms.date: 07/03/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7e65b4cd98eec0588637899c148dc14e79db67ec
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547370"
---
# <a name="boot-options-in-a-bootini-file"></a>Boot.ini 文件中的启动选项

> [!IMPORTANT] 
> 本主题介绍支持 Windows XP 和 Windows Server 2003 中的启动选项。 如果要更改为 Windows 8、 Windows Server 2012、 Windows 7、 Windows Server 2008 或 Windows Vista 的启动选项，请参阅[Windows Vista 和更高版本中的启动选项](boot-options-in-windows-vista-and-later.md)。\]

Boot.ini 是系统分区，通常为 c： 根目录的文本文件\\Boot.ini。 Boot.ini 存储启动传统上，基于 IA-32 的和基于 x64 的处理器的计算机具有 BIOS 固件的计算机的选项。 在 Windows Server 2003 和早期版本的 Windows NT 系列的操作系统上，在计算机启动时，Windows 启动加载器，名为"ntldr"、 Boot.ini 文件中读取和显示启动菜单中的每个操作系统条目。 然后，ntldr 加载 Boot.ini 文件中的设置根据选择的操作系统。

默认情况下，在 NTFS 驱动器上**系统**，**隐藏**，**存档**，以及**只读**属性设置为保护 Boot.ini; 但是，Administrators 组的成员可以更改这些属性。 文件属性不会影响启动加载程序的操作。

以下各节简要介绍了 Boot.ini 并解释特定于个人计算机高级技术的计算机的启动选项的方面 (PC / AT)-键入 BIOS 固件。

本部分包括：

- [Boot.ini 文件的概述](overview-of-the-boot-ini-file.md)
- [编辑 Boot.ini 文件](editing-the-boot-ini-file.md)
- [Boot.ini 文件备份](backing-up-the-boot-ini-file.md)

本文档介绍 Boot.ini 的驱动程序开发人员和测试人员特别重要的方面。 Boot.ini 参数的完整列表，请参阅[可用的交换机选项适用于 Windows XP 和 Windows Server 2003 Boot.ini 文件](https://go.microsoft.com/fwlink/p/?linkid=137742)Microsoft 支持网站上的主题。
