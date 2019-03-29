---
title: 设置文本日志的目录路径
description: 设置文本日志的目录路径
ms.assetid: d56a8f6c-365b-427d-b965-65616ede3d7e
keywords:
- 文本日志 WDK SetupAPI，目录路径
- 目录路径 WDK SetupAPI 日志记录
- LogPath
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f923094189d30b9515fde20843eb624102e2d8b3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567452"
---
# <a name="setting-the-directory-path-of-the-text-logs"></a>设置文本日志的目录路径


默认情况下，安装程序 Api 文本日志位于系统 Windows 目录中。 可以通过设置以下更改 SetupAPI 文本日志的位置[REG_SZ](https://docs.microsoft.com/windows/desktop/SysInfo/registry-value-types)注册表值：

**HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Setup\\LogPath**

**LogPath**注册表值必须是完全限定的目录路径。 路径必须存在，并且该路径不能包含文件名称。

如果**LogPath**注册表值不存在、 路径不存在，或该路径包括文件名、 SetupAPI 查找中的文本日志 *%SystemRoot%/Inf*目录。

 

 





