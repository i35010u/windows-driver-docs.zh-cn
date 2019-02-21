---
title: 使用 Visual SourceSafe
description: 使用 Visual SourceSafe
ms.assetid: a315a1c5-1427-4432-aec0-314dbb6d7ae5
keywords:
- Visual SourceSafe
- Visual SourceSafe 的源服务器
- SrcSrv，Visual SourceSafe
- Visual SourceSafe, SrcSrv
- Visual SourceSafe 概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e01291cad2de04560bff449c193966648c1e82c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519612"
---
# <a name="using-visual-sourcesafe"></a>使用 Visual SourceSafe


Visual SourceSafe 是基于 x86 的应用程序，并仅与 x86 安装的源索引编制脚本和工具与之关联的 Windows 调试工具的包。

若要成功使用 SrcSrv Visual SourceSafe，必须在系统中，包括 Visual SourceSafe 默认数据库、 当前项目中，和工作文件夹设置几个默认值。 以便 Visual SourceSafe 可以区分给定文件的版本，还必须使用标签标记每个生成项目。 最后，必须设置访问 Visual SourceSafe 数据库所需的任何凭据。

### <a name="span-idvisualsourcesafedatabasespanspan-idvisualsourcesafedatabasespanvisual-sourcesafe-database"></a><span id="visual_sourcesafe_database"></span><span id="VISUAL_SOURCESAFE_DATABASE"></span>Visual SourceSafe 数据库

默认 Visual SourceSafe 数据库可以与 SSDIR 环境变量设置。 如果该设置不存在，SrcSrv 索引脚本通常可以确定这从注册表。 如果不能脚本会提示您设置 SSDIR。 无论如何，此数据库值必须列在您[Srcsrv.ini](the-srcsrv-ini-file.md)文件和简单的别名来标识数据库。 可以在 Srcsrv.ini 中的注释中找到详细说明。 您应使用以下语法的 Srcsrv.ini 的变量部分中添加条目：

```ini
MYDATABASE=\\server\VssShare
```

### <a name="span-idcurrentprojectspanspan-idcurrentprojectspancurrent-project"></a><span id="current_project"></span><span id="CURRENT_PROJECT"></span>当前项目

Visual SourceSafe 使用的概念*当前项目*。 此值和限制到当前项目的一部分这些源文件处理会遵守 SrcSrv 索引脚本。 若要显示当前项目，请使用以下命令：

```console
ss.exe project
```

若要更改当前项目，请使用以下命令：

```console
ss.exe cp Project
```

其中*项目*指示当前的项目。 例如，若要处理的所有项目，将当前项目设置为根目录：

```console
ss.exe cp $/
```

### <a name="span-idworkingfolderspanspan-idworkingfolderspanworking-folder"></a><span id="working_folder"></span><span id="WORKING_FOLDER"></span>工作文件夹

与 visual SourceSafe 项目相关联*工作文件夹*。 工作文件夹是与项目的根相对应的客户端计算机上的位置。 但是，此类计算机获取并不创建项目的 Visual Studio 接口也可以使用该命令时通常所指定的工作文件夹的情况下生成源可以：

```console
ss.exe get -R
```

但是，此操作模式不兼容，以及 SrcSrv 的索引。 SrcSrv 要求指定的工作文件夹。 若要设置的工作文件夹，请使用命令：

```console
ss.exe workfold Project Folder
```

其中*项目*指示当前项目并*文件夹*指示对应于项目的根目录的位置。

### <a name="span-idlabelsspanspan-idlabelsspanlabels"></a><span id="labels"></span><span id="LABELS"></span>标签

Visual SourceSafe 无法确定哪个版本的文件在生成计算机的工作目录中存在。 因此，必须使用标签来戳记该项目与用于提取调试器客户端上的源文件的标识符。 因此，在编制索引之前, 必须验证所有更改已签入到数据库，然后将标签应用到项目。 可以使用该命令应用标签：

```console
ss.exe label Project
```

其中*项目*指示当前的项目。

在下面的示例中，标签"版本\_3"应用于名为"$/ sdktools"的项目：

```console
E:\nt\user>ss.exe label $/sdktools
 Label for $/sdktools: VERSION_3
 Comment for $/sdktools:
 This is a comment.
```

应用标签后，可以指定此标签到 SrcSrv 索引脚本，通过设置环境变量，SSLABEL，或将其传递为命令行参数，如以下示例所示：

```console
vssindex.cmd -label=VERSION_3
```

同样，此标签是必需的 SrcSrv 索引来起作用。 请注意，是否通过项目中不存在的标签，可能需要很长时间才能完成的脚本，结果将是没有用处。

### <a name="span-idcredentialsspanspan-idcredentialsspancredentials"></a><span id="credentials"></span><span id="CREDENTIALS"></span>凭据

如果 Visual SourceSafe 数据库需要的访问权限的用户和可选密码，则必须通过 SSUSER 和 SSPWD 环境变量设置这些值。 这适用时生成的编制索引的索引，不仅调试器客户端上。

 

 





