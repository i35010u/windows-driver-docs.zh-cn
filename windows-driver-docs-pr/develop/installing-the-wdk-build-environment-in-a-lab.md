---
ms.assetid: D4B35683-5BD1-40F8-9734-95DADF9E0F20
title: 在实验室中安装 WDK 生成环境
description: Windows 驱动程序工具包 (WDK) 8.1 使你可以将 Visual Studio 和 WDK 的组件复制到新位置，然后通过命令行启动生成环境。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5072737d94c1546f29953147edbdf8b44304929d
ms.sourcegitcommit: 5598b4c767ab56461b976b49fd75e4e5fb6018d2
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2020
ms.locfileid: "63344856"
---
# <a name="installing-the-wdk-81-build-environment-in-a-lab"></a>在实验室中安装 WDK 8.1 生成环境

Windows 驱动程序工具包 (WDK) 8.1 中提供的功能使你可以将 Visual Studio 和 WDK 的组件复制到新位置，然后通过命令行启动生成环境。 通过此环境，你无需运行 Visual Studio 或 WDK 安装程序即可生成 Windows 驱动程序。

如果你需要将 WDK 与生成流程集成，或者你想要在实验室或测试环境中分配生成流程，那么，你将会发现此功能非常有用。

**注意**  你仅可将此功能用于生成使用 C 和 C++ 的驱动程序和应用程序。 此功能不可用于托管代码或 UWP 应用。


## <a name="1-download-the-visual-studio-and-wdk-and-sdk-setup-files"></a>1.下载 Visual Studio 以及 WDK 和 SDK 安装文件


若要运行支持此功能的设置脚本，你需要提供 Visual Studio 和 WDK 安装文件的路径。 请务必保存这些文件（而不是安装它们）。

1.  下载 [Visual Studio Professional 2013](https://go.microsoft.com/fwlink/p/?linkid=316548) 或 [Visual Studio Ultimate 2013](https://go.microsoft.com/fwlink/p/?linkid=316520)。 下载产品布局（例如，vs\_ultimate\_download.exe）。 当系统询问你是想要运行还是保存 vs\_ultimate\_download.exe 时，单击“运行”  并选择下载选项，然后将下载路径指定为 **C:\\VSSetup**（这将简化后续步骤）。 单击“下载”  将 DVD 布局的本地副本下载并安装到计算机上。
2.  下载独立的 [SDK](https://go.microsoft.com/fwlink/p/?linkid=323507)。 当系统询问你是想要运行还是保存 sdksetup.exe 时，单击“运行”  ，然后将下载位置指定为 **C:\\Kits\\SDK**。 单击“下一步”  并按照说明下载独立的 SDK。
3.  下载 [WDK 8.1](https://go.microsoft.com/fwlink/p/?linkid=317353)。 当系统询问你是想要运行还是保存 wdksetup.exe 时，单击“运行”  ，然后将下载位置指定为 **C:\\Kits\\WDK**。 单击“下一步”  并按照说明下载 WDK。 如果已在计算机上安装 WDK，则 web 安装程序将会告诉你计算机上安装的功能已处于最新状态。 若要下载 WDK 设置文件以便能够部署生成环境，请单击“下一步”  并指定 **C:\\Kits\\WDK** 路径。

## <a name="span-iddownload_scriptspanspan-iddownload_scriptspan2-download-the-buildlabsupport-files"></a><span id="download_script"></span><span id="DOWNLOAD_SCRIPT"></span>2.下载 BuildLabSupport 文件


若要能够在实验室的计算机上安装 WDK 生成环境，你需要先在计算机上下载生成实验室支持文件。

1.  下载 [BuildLabSupportfiles.zip](https://go.microsoft.com/fwlink/p/?linkid=321805)。
2.  将压缩文件的内容提取到计算机上。 提取的文件包括 BuildLabSupport 目录及你需要的设置文件和实用程序。

## <a name="span-idinstall_scriptspanspan-idinstall_scriptspan3-install-the-wdk81-build-environment"></a><span id="install_script"></span><span id="INSTALL_SCRIPT"></span>3.安装 WDK 8.1 生成环境


生成实验室支持文件包括 **setup.ps1** PowerShell 命令文件，它将提取所需的 Visual Studio 和 WDK 组件并将其复制到目标目录（文件夹）。 随后，你可以将此目录复制到另一个位置，从此位置你可以在 Visual Studio 命令行接口 (CLI) 开发环境中生成项目。

-   使用提升的权限打开命令提示符（**以管理员身份运行**），并转至你提取生成实验室支持文件的目录。 PowerShell 命令脚本 **setup.ps1** 位于 &lt;*root*&gt;\\BuildLabSupport 目录中。

    PowerShell 命令的语法如下：

    <span codelanguage="PowerShell"></span>
    <table>
    <colgroup>
    <col width="100%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">PowerShell</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><pre><code>powershell –executionpolicy bypass –file Setup.ps1 –DeployBuildLab –VSInstallerPath &lt;VSInstallerFilePath&gt; -KitInstallersPath &lt;KitInstallersPath&gt; -ExpansionRoot &lt;Target Directory&gt; –LogFilePath &lt;LogFilePath&gt; -CatalogFile &lt;Filename.xml&gt;</code></pre></td>
    </tr>
    </tbody>
    </table>

    -   *&lt;VSInstallerFilePath&gt;* 是 Visual Studio 安装程序（例如，Vs\_ultimate.exe）和包含产品布局的目录的路径。
    -   *&lt;KitInstallersPath&gt;* 是 WDK 和 SDK 安装文件的路径。
    -   *&lt;Target Directory&gt;* 是所提取内容的目标目录。
    -   *&lt;LogFilePath&gt;* 是日志文件的目标位置。
    -   *&lt;Filename.xml&gt;* 是 CatalogFile 的名称，它包含作为安装的一部分扩展的 Microsoft Windows 安装文件 (MSI) 的列表。 文件名为 files.xml。

    例如，以下命令将运行 BuildLabSupport 目录中的脚本并将生成环境安装于 C:\\BuildLabInstall 目录中。

    ```cpp
    c:\BuildLabSupport>powershell -executionpolicy bypass -file Setup.ps1 -DeployBuildLab -VSInstallerPath c:\VSSetup -KitInstallersPath c:\Kits -E
    xpansionRoot C:\BuildLabInstall -CatalogFile  files.xml
    ```

## <a name="span-idbuild_stepspanspan-idbuild_stepspan4-build-windows-driver-projects-and-solutions"></a><span id="build_step"></span><span id="BUILD_STEP"></span>4.生成 Windows 驱动程序项目和解决方案


**使用生成环境命令脚本**

1.  打开“命令提示符”窗口。 找到目标目录中的 LaunchBuildEnv.cmd 文件（例如，C:\\BuildLabInstall）。
2.  通过运行 **LaunchBuildEnv.cmd** 启动生成环境。
3.  使用 MSBuild 命令生成驱动程序项目和解决方案。 例如：

    ```cpp
    msbuild /t:clean /t:build .\MyDriver.vcxproj /p:Configuration="Win8.1 Debug" /p:Platform=Win32
    ```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


* [生成驱动程序](building-a-driver.md)
* [MSBuild](https://go.microsoft.com/fwlink/p/?linkid=262804)
 

 






