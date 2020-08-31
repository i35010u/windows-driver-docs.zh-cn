---
title: 设置文本日志的目录路径
description: 设置文本日志的目录路径
ms.assetid: d56a8f6c-365b-427d-b965-65616ede3d7e
keywords:
- 文本日志 WDK Setupapi.log，目录路径
- 目录路径 WDK Setupapi.log 日志记录
- LogPath
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdbdf6f03467ab23d983ba2a651c5781954a96c8
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096639"
---
# <a name="setting-the-directory-path-of-the-text-logs"></a>设置文本日志的目录路径


默认情况下，Setupapi.log 文本日志位于系统 Windows 目录中。 可以通过设置以下 [REG_SZ](/windows/desktop/SysInfo/registry-value-types) 注册表值来更改 setupapi.log 文本日志的位置：

**HKEY_LOCAL_MACHINE \\ Software \\ Microsoft \\ Windows \\ CurrentVersion \\ 安装程序 \\ LogPath**

**LogPath**注册表值必须为完全限定的目录路径。 路径必须存在，并且路径不能包含文件名。

如果 **LogPath** 注册表值不存在，路径不存在，或者路径包含文件名，则 setupapi.log 将在 *% SystemRoot%/Inf* 目录中查找文本日志。

 

