---
title: 设置文本日志的目录路径
description: 设置文本日志的目录路径
keywords:
- 文本日志 WDK Setupapi.log，目录路径
- 目录路径 WDK Setupapi.log 日志记录
- LogPath
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 082f5ac3e1c4960eb5254185b531dccc584f1945
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816655"
---
# <a name="setting-the-directory-path-of-the-text-logs"></a>设置文本日志的目录路径


默认情况下，Setupapi.log 文本日志位于系统 Windows 目录中。 可以通过设置以下 [REG_SZ](/windows/desktop/SysInfo/registry-value-types) 注册表值来更改 setupapi.log 文本日志的位置：

**HKEY_LOCAL_MACHINE \\ Software \\ Microsoft \\ Windows \\ CurrentVersion \\ 安装程序 \\ LogPath**

**LogPath** 注册表值必须为完全限定的目录路径。 路径必须存在，并且路径不能包含文件名。

如果 **LogPath** 注册表值不存在，路径不存在，或者路径包含文件名，则 setupapi.log 将在 *% SystemRoot%/Inf* 目录中查找文本日志。

 

