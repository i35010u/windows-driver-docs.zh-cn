---
title: 使用 Visual SourceSafe 进行调试
description: 使用 Visual SourceSafe 进行调试
ms.assetid: 65cc4eda-7aed-489f-a622-27a42afc0e4a
keywords:
- Visual SourceSafe 中，调试
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: c51bcaa59549706d4dba145703e77408299e5e18
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63346319"
---
# <a name="debugging-with-visual-sourcesafe"></a>使用 Visual SourceSafe 进行调试


为了使源代码文件编制索引使用 Visual SourceSafe 与调试器一起正常工作，必须正确配置您的系统。

如果 Visual SourceSafe 数据库需要的访问权限的用户和可选密码，必须使用在 SSUSER 和 SSPWD 环境变量设置这些值。 此外，使用 Visual Studio 2005 SrcSrv 附带的版本无法检测是否 Visual SourceSafe 提示输入凭据时，这会导致应用程序停止响应... 升级到与调试工具的 Windows 为防止这种 SrcSrv 附带的版本。

如果 Visual SourceSafe 未设置在调试的计算机的路径中，您可以通过将项添加到获取对此进行演练[Srcsrv.ini](the-srcsrv-ini-file.md)适用于您的调试器的文件。 使用 Visual Studio 的标准安装时，此文件应位于

```text
%PROGRAMFILES%\Microsoft Visual Studio 8\Common7\IDE\srcsrv.ini
```

在中\[受信任的命令\]部分的 Srcsrv.ini，添加窗体的一个条目

```ini
ss.exe="Path"
```

其中*路径*是 Ss.exe 的位置。

 

 





