---
title: 使用 Visual SourceSafe 进行调试
description: 使用 Visual SourceSafe 进行调试
keywords:
- Visual SourceSafe，调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f30ff989dd91a8a38b3ec24105f5dd6f8950f8f2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785277"
---
# <a name="debugging-with-visual-sourcesafe"></a>使用 Visual SourceSafe 进行调试


为了使使用 Visual SourceSafe 建立索引的源文件能在调试器中正常工作，必须正确地配置系统。

如果 Visual SourceSafe 数据库需要用户和可选密码才能访问，则必须使用 SSUSER 和 SSPWD 环境变量设置这些值。 此外，Visual Studio 2005 附带的 Srcsrv.ini 版本无法检测 Visual SourceSafe 是否会提示输入凭据，从而导致应用程序停止响应。 升级到随 Windows 调试工具附带的 Srcsrv.ini 版本，以防止出现这种情况。

如果未在调试计算机的路径中设置 Visual SourceSafe，则可以通过将条目添加到适用于调试器的 [Srcsrv.ini](the-srcsrv-ini-file.md) 文件中来解决此问题。 使用 Visual Studio 的标准安装时，此文件应位于

```text
%PROGRAMFILES%\Microsoft Visual Studio 8\Common7\IDE\srcsrv.ini
```

在 Srcsrv.ini 的 " \[ 受信任的命令" \] 部分中，添加表单的条目

```ini
ss.exe="Path"
```

其中 *Path* 是 Ss.exe 的位置。

 

 





