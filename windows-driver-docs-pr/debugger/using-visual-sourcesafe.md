---
title: 使用 Visual SourceSafe
description: 使用 Visual SourceSafe
keywords:
- Visual SourceSafe
- 源服务器，Visual SourceSafe
- Srcsrv.ini，Visual SourceSafe
- Visual SourceSafe，Srcsrv.ini
- Visual SourceSafe，概述
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5b7cc29499936cb5a186f8b126496ac253902ea
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802989"
---
# <a name="using-visual-sourcesafe"></a>使用 Visual SourceSafe


Visual SourceSafe 是基于 x86 的应用程序，而与之关联的源索引脚本和工具仅与 Windows 调试工具的 x86 包一起安装。

若要成功地将 Visual SourceSafe 与 Srcsrv.ini 一起使用，必须在系统中设置多个默认值，包括 Visual SourceSafe 默认数据库、当前项目和工作文件夹。 还必须使用标签标记每个生成项目，以便 Visual SourceSafe 可以区分给定文件的版本。 最后，必须设置访问 Visual SourceSafe 数据库所需的任何凭据。

### <a name="span-idvisual_sourcesafe_databasespanspan-idvisual_sourcesafe_databasespanvisual-sourcesafe-database"></a><span id="visual_sourcesafe_database"></span><span id="VISUAL_SOURCESAFE_DATABASE"></span>Visual SourceSafe 数据库

可以通过 SSDIR 环境变量设置默认的 Visual SourceSafe 数据库。 如果未在此设置，Srcsrv.ini 索引脚本通常可以从注册表确定这一点。 如果不能，该脚本将提示你设置 SSDIR。 无论如何，此数据库值都必须在 [Srcsrv.ini](the-srcsrv-ini-file.md) 文件中列出，并且还必须列出一个简单的别名来标识数据库。 Srcsrv.ini 中的注释可以找到更多说明。 应使用以下语法在 Srcsrv.ini 的 variables 节中添加条目：

```ini
MYDATABASE=\\server\VssShare
```

### <a name="span-idcurrent_projectspanspan-idcurrent_projectspancurrent-project"></a><span id="current_project"></span><span id="CURRENT_PROJECT"></span>当前项目

Visual SourceSafe 使用 *当前项目* 的概念。 Srcsrv.ini 索引脚本会遵守此值，并将处理限制为作为当前项目一部分的源文件。 若要显示当前项目，请使用以下命令：

```console
ss.exe project
```

若要更改当前项目，请使用以下命令：

```console
ss.exe cp Project
```

其中， *project* 指示当前项目。 例如，若要处理所有项目，请将当前项目设置为根：

```console
ss.exe cp $/
```

### <a name="span-idworking_folderspanspan-idworking_folderspanworking-folder"></a><span id="working_folder"></span><span id="WORKING_FOLDER"></span>工作文件夹

Visual SourceSafe 项目与 *工作文件夹* 关联。 工作文件夹是客户端计算机上与项目的根对应的位置。 但是，这种计算机在未指定工作文件夹的情况下（通常在通过 Visual Studio 界面或使用命令创建项目时），可以获取和生成源：

```console
ss.exe get -R
```

但是，此操作模式与 Srcsrv.ini 索引不兼容。 Srcsrv.ini 要求指定工作文件夹。 若要设置工作文件夹，请使用命令：

```console
ss.exe workfold Project Folder
```

其中， *project* 指示当前项目， *文件夹* 指示与项目的根对应的位置。

### <a name="span-idlabelsspanspan-idlabelsspanlabels"></a><span id="labels"></span><span id="LABELS"></span>标志

Visual SourceSafe 无法确定生成计算机的工作目录中存在文件的哪个版本。 因此，您必须使用标签来标记项目，其中标识符用于在调试器客户端上提取源文件。 因此，在编制索引之前，必须验证所有更改是否已签入数据库，然后将标签应用到项目。 可以使用命令应用标签：

```console
ss.exe label Project
```

其中， *project* 指示当前项目。

在下面的示例中，"版本 \_ 3" 标签应用于名为 "$/sdktools" 的项目：

```console
E:\nt\user>ss.exe label $/sdktools
 Label for $/sdktools: VERSION_3
 Comment for $/sdktools:
 This is a comment.
```

应用标签后，您可以通过设置环境变量或 SSLABEL 或将其作为命令行参数传递，为 Srcsrv.ini 索引脚本指定此标签，如以下示例中所示：

```console
vssindex.cmd -label=VERSION_3
```

同样，若要运行 Srcsrv.ini 索引，此标签是必需的。 请注意，如果传递的标签在项目中不存在，则脚本可能需要很长时间才能完成，并且结果不使用。

### <a name="span-idcredentialsspanspan-idcredentialsspancredentials"></a><span id="credentials"></span><span id="CREDENTIALS"></span>凭据

如果 Visual SourceSafe 数据库需要用户和可选密码才能访问，则必须通过 SSUSER 和 SSPWD 环境变量设置这些值。 这不仅适用于对生成编制索引的时间，还适用于调试器客户端。

 

 





