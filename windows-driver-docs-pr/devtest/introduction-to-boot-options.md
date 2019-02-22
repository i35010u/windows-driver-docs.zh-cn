---
title: 介绍启动选项
description: 运行 Microsoft Windows 操作系统的所有计算机上非常类似的概念和内容的启动选项。
ms.assetid: e8e835c4-75de-4ce1-965f-d9b822e15044
keywords:
- 有关启动选项启动选项 WDK，
- 存储启动选项
- 启动加载程序 WDK
ms.date: 07/02/2018
ms.localizationpriority: medium
ms.openlocfilehash: d65ab2b31d8f6b885bb017f4ca678eb1985cd80b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547114"
---
# <a name="introduction-to-boot-options"></a>介绍启动选项

运行 Microsoft Windows 操作系统的所有计算机上非常类似的概念和内容的启动选项。 但是，在 Windows Vista 之前具有不同处理器固件的计算机以不同的方式存储启动选项，并且需要不同的工具来查看和编辑每个系统上的选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Windows 版本</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><span id="______Windows_7__Windows_Server_2008__Windows_Vista"></span><span id="______windows_7__windows_server_2008__windows_vista"></span><span id="______WINDOWS_7__WINDOWS_SERVER_2008__WINDOWS_VISTA"></span>Windows Server 2016 中，Windows 10、 Windows Server 2012 R2、 Windows 8.1、 Windows Server 2012 中，Windows 8、 Windows Server 2008 R2、 Windows 7、 Windows Server 2008、 Windows Vista</p></td>
<td align="left"><p>Windows Vista 和更高版本的 Windows，请在不依赖固件的存储和配置系统中存储启动选项。 Windows Vista 还引入了新的启动管理器和特定于系统的引导加载程序。 有关详细信息，请参阅<a href="boot-options-in-windows-vista-and-later.md" data-raw-source="[Boot Options in Windows Vista and Later](boot-options-in-windows-vista-and-later.md)">Windows Vista 和更高版本中的启动选项</a>。</p></td>
</tr>
</tbody>
</table>

本部分包括：
- [Boot.ini 文件中启动选项](boot-options-in-a-boot-ini-file.md)（Windows XP、 Windows Server 2003）
- [在 EFI NVRAM 启动选项](boot-options-in-efi-nvram.md)（Windows XP、 Windows Server 2003）
- [在 Windows Vista 及更高版本的启动选项的概述](boot-options-in-windows-vista-and-later.md)
