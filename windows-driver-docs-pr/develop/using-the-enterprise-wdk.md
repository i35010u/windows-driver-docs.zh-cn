---
title: 使用企业版 WDK 10
description: 介绍如何设置基于命令行的环境，以便组织使用 WDK。
ms.date: 08/25/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66ff7c0eaafd4f96cc5cb33faafe5ceffa168611
ms.sourcegitcommit: ee3e2259aafc844cc43cce62299a72649cf89212
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "91353656"
---
# <a name="using-the-enterprise-wdk-10"></a>使用企业版 WDK 10

企业版 Windows 驱动程序工具包（企业版 WDK）是一个在使用之前无需任何安装的命令行生成环境。  下载 EWDK 后，你可以使用版本控制软件进行管理或者根据需要压缩文件并进行复制。  使用企业版 WDK 创建的 .zip 文件包含生成基于 Visual Studio 的驱动程序项目所需的所有编译器、链接器、生成工具、头文件和库。

企业版 WDK 包含生成驱动程序和基本 Win32 驱动程序测试应用程序所需的元素。  使用你喜爱的代码编辑器来修改源代码和项目文件。  由于企业版 WDK 基于命令行，因此，它缺少 Visual Studio 中所含的部分功能，例如 IDE、驱动程序部署和驱动程序测试。 



## <a name="getting-started"></a>入门

> [!NOTE] 
> 从 Windows 10 1709 版本开始，企业版 WDK 基于 ISO。  若要开始使用，请下载并装载 ISO，然后运行 `LaunchBuildEnv`。

1.  从以下位置下载 EWDK：[WDK 和 EWDK 下载](../download-the-wdk.md)
2.  将 .zip 文件展开到一个适当命名的目录中，例如 d:\ewdk。
3.  在管理员命令提示符下，导航到上一步中的展开文件夹，然后运行 **LaunchBuildEnvcmd** 以创建生成环境。 例如：**D:\EWDK\LaunchBuildEnv**

创建生成环境后，你可以使用其操作文件或生成 Visual Studio 项目。 例如，  
*   Cd *directory_containing_project_files*
*   Msbuild *projectname*.vsproj

用于项目和解决方案的基本 MSBuild 命令：
* Msbuild project.vcxproj /p:configuration=[release | debug] /p:platform=[arm | Win32 | x64]

若要创建桌面快捷方式：

%comspec% /k pushd `<drive\dir>` && LaunchBuildEnv.cmd

其中，`<drive\dir>` 为文件被提取到的位置，如 d:\ewdk

%comspec% /k pushd "d:\ewdk" && LaunchBuildEnv.cmd


## <a name="see-also"></a>另请参阅

[MSBuild 参考](/visualstudio/msbuild/msbuild-reference?view=vs-2015)