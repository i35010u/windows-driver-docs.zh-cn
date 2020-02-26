---
title: 生成基本的 v4 打印机驱动程序
description: 使用 Microsoft Visual Studio 2017 中的驱动程序开发向导来生成一个基本 v4 打印机驱动程序，以选择创建功能打印机驱动程序的最小功能集。
ms.assetid: 6E50CD69-D385-4724-B6B1-85D42EFFC6F0
ms.date: 02/25/2020
ms.localizationpriority: medium
ms.openlocfilehash: 5eec5a853f2c555883f14522245d4a9d4a894854
ms.sourcegitcommit: a54b96c52b0c7009dfa05bcc68d210b13711f2ea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/25/2020
ms.locfileid: "77601731"
---
# <a name="building-a-basic-v4-printer-driver"></a>生成基本的 v4 打印机驱动程序

使用 Microsoft Visual Studio 2017 中的驱动程序开发向导来生成一个基本 v4 打印机驱动程序，以选择创建功能打印机驱动程序的最小功能集。

本主题中的说明将重点介绍构建驱动程序所需的步骤，而不会介绍向导中提供的许多打印机驱动程序选项。 本主题的目的是介绍在 Visual Studio 2017 中开发打印机驱动程序时所涉及的过程。 有关打印机驱动程序选项的详细信息，请参阅[浏览向导中的驱动程序选项](exploring-the-driver-options-in-the-wizard.md)。

## <a name="instructions"></a>说明

### <a name="select-features-for-the-basic-driver"></a>选择基本驱动程序的功能

1. 在 Visual Studio 的主菜单中，单击 "**文件**" &gt;**新建**&gt;**项目**"。

2. 在 "**新建项目**" 窗口中，在右上方的搜索框中键入 "*打印机驱动程序 v4* "，然后按 enter。 这将检索名称中包含搜索文本的所有驱动程序模板。

3. 在中间窗格中，选择 "**打印机驱动程序 V4**"。

4. 在 "**名称**" 字段中键入驱动程序的名称，然后单击 **"确定"** 。 例如，可以键入 " *MyV4PrintDriver*"。

5. 在**创建 V4 打印驱动程序向导**中的 "**选择驱动程序呈现类型：** " 下，单击 "**使用自定义呈现筛选器的 v4 打印驱动程序" （仅接受 XPS）** 。

6. 将所有其他选项保留默认设置，然后单击 "**下一步**"。

7. 在向导的 "**安装信息**" 部分中，保留所有选项的默认设置，然后单击 "**下一步**"。

8. 在向导的 "**安装信息（第2页）** " 部分中，保留所有选项的默认设置，然后单击 "**下一步**"。

Microsoft Visual Studio 使用前面的选项来生成*MyV4PrintDriver*的项目文件。

### <a name="verify-the-generated-driver-files"></a>验证生成的驱动程序文件

1. 导航至生成的驱动程序文件所在的文件夹。 例如，如果你将项目命名为*MyV4PrintDriver*，则默认情况下，文件将保存到以下位置： *"我的文档" &gt; Visual Studio 2017 &gt; 项目 &gt; MyV4PrintDriver &gt; MyV4PrintDriver*。

2. 验证文件夹是否包含以下文件：

    | 文件名称                                              | 文件类型                                                  |
    |--------------------------------------------------------|------------------------------------------------------------|
    | MyV4PrintDriver.gpd                                    | 打印机说明文件                                   |
    | MyV4PrintDriver .inf                                    | 安装信息文件                                     |
    | MyV4PrintDriver. .vcxproj                                | C++项目文件                                           |
    | MyV4PrintDriver. .vcxproj                        | C++项目筛选器文件                                   |
    | MyV4PrintDriver-manifest                           | 配置设置文件（也称为 打印驱动程序清单） |
    | V4PrintDriver-Intellisense                          | Intellisense 的 JavaScript 文件                           |
    | V4PrintDriver-Intellisense-Windows 8.1 .js               | Intellisense 的 JavaScript 文件                           |

请注意，上表中有一个创建的文件是一个 INF 文件。 请注意，Visual Studio 创建了一个需要完成的框架 INF 文件，以便可以使用它来安装驱动程序。

### <a name="create-a-unique-printerdriverid-for-the-driver"></a>为驱动程序创建唯一的**PrinterDriverID**

1. 在 "Visual Studio Tools" 菜单中选择 "**创建 GUID**"。

2. 选择选项**4。注册表格式**，然后单击 "**复制**" 按钮。

3. 在 Visual Studio 的 "解决方案资源管理器中，展开" *MyV4PrintDriver* "节点。

4. 单击 "**驱动程序文件**"，然后在 "**属性**" 窗口中查看 "*唯一标识符*" 字段的值。 将此值替换为使用**Paste**生成的 GUID。

### <a name="complete-the-inf-file"></a>完成 INF 文件

在 MyV4PrintDriver 项目中，应存在**驱动程序文件**的条目。 打开此文件，应列出 MyV4PrintDriver 文件。 打开此文件。

#### <a name="1-update-the-copyright-notice"></a>1. 更新版权声明

INF 文件的前2行是驱动程序包的版权声明。

第1行包含公司的年和名称。 将字符 YYYY 替换为当前年份，并将 &lt;*制造商名称*&gt; 的字符替换为公司名称。

第2行介绍了驱动程序 INF 的内容，包括制造商名称和设备型号信息。 将 &lt;*制造商名称*&gt; 的字符替换为公司名称，并将 &lt;*打印机型号*&gt; 中的字符替换为驱动程序支持的打印机型号名称。

例如，如果年份为2017，公司名称为 Fabrikam，打印设备型号为1234，则可以键入以下内容：

```inf
; Copyright (c) 2017 Fabrikam
; INF file for the Fabrikam 1234 print driver
```

#### <a name="2-verify-the-version-section-is-correct"></a>2. 验证 **\[版本\]** 部分是否正确

找到包含 **\[版本\]** 的行。

- 检查并确保显示以下行：

    ```inf
    **ClassVer**=4.0
    ```

- 检查并确保显示以下行：

    ```inf
    **Signature**="$WINDOWS NT$"
    ```

#### <a name="3-configure-the-sourcedisksfiles-section"></a>3. 配置 **\[SourceDisksFiles\]** 部分

找到包含 **\[SourceDisksFiles\]** 的行。

在此键入以下行：

```inf
MyV4PrintDriver.gpd=1
MyV4PrintDriver-manifest.ini=1
MyV4PrintDriverRenderFilter-PipelineConfig.xml=1
MyV4PrintDriverRenderFilter.dll=1
```

#### <a name="4-configure-the-driverfiles-section"></a>4. 配置 **\[DriverFiles\]** 部分

找到包含 **\[DriverFiles\]** 的行。

在此键入以下行：

```inf
MyV4PrintDriver.gpd
MyV4PrintDriver-manifest.ini
MyV4PrintDriverRenderFilter-PipelineConfig.xml
MyV4PrintDriverRenderFilter.dll
```

#### <a name="5-configure-the-standardntarch-section"></a>5. 配置 **\[Standard. NT $** $ $ $ $\]部分

找到包含 **\[Standard. NT $ $ $ $ $\]** 的行。

本部分引用每个模型的 INF 的 "安装" 部分。 例如，如果您的打印机型号为 Fabrikam 1234，则可以键入以下内容：

```inf
"Fabrikam 1234"=DriverInstall, USBPRINT\\Fabrikam1234
"Fabrikam 1234"=DriverInstall, WSDPRINT\\Fabrikam1234
```

#### <a name="6-add-printerdriverid-to-the-inf-file"></a>6. 将**PrinterDriverID**添加到 INF 文件

在 Visual Studio 的 "解决方案资源管理器中，展开" *MyV4PrintDriver* "节点。

单击 "**驱动程序文件**"，然后在 "**属性**" 窗口中查看 "*唯一标识符*" 字段的值。 这是驱动程序 ID （GUID）。 突出显示并复制

在 INF 文件中，在 **\[Standard. NT $ $ $ $\]** 部分中，键入以下行：

```inf
"Fabrikam 1234"=DriverInstall,
```

然后在逗号后，粘贴在上一步中复制的 GUID。 已完成的 **\[Standard. NT $ $ $\]** 部分应如下所示：

```inf
"Fabrikam 1234"=DriverInstall, {GUID}
"Fabrikam 1234"=DriverInstall, USBPRINT\Fabrikam1234
"Fabrikam 1234"=DriverInstall, WSDPRINT\Fabrikam1234
```

#### <a name="7-configure-the-strings-section"></a>7. 配置 **\[字符串\]** 部分

查找 **\]包含\[字符串**的行。

在此，你将找到*ManufacturerName*字符串的定义。 将 &lt;制造商名称&gt; 的字符替换为公司名称，以提供制造商的目标打印机名称并删除包含的行的其余部分;做

例如，如果你的公司名称为 Fabrikam，你可以键入以下内容：

```inf
ManufacturerName="Fabrikam"
```

#### <a name="8-save-the-inf-file"></a>8. 保存 INF 文件

完成 INF 文件后，该文件应如下所示：

```inf
; Copyright (c) 2017 Fabrikam
; INF file for the Fabrikam 1234 print driver

[Version]
Signature="$Windows NT$"
Class=Printer
ClassGuid={4D36E979-E325-11CE-BFC1-08002BE10318}
Provider=%ManufacturerName%
CatalogFile=MyV4PrintDriver.cat
ClassVer=4.0
DriverVer=03/17/2014,1.0.0.0

[Manufacturer]
%ManufacturerName%=Standard,NT$ARCH$

[Standard.NT$ARCH$]
"Fabrikam 1234"=DriverInstall, {GUID}
"Fabrikam 1234"=DriverInstall, USBPRINT\Fabrikam1234
"Fabrikam 1234"=DriverInstall, WSDPRINT\Fabrikam1234

[DriverInstall]
CopyFiles=DriverFiles

[DriverFiles]
MyV4PrintDriver.gpd
MyV4PrintDriver-manifest.ini
MyV4PrintDriverRenderFilter-PipelineConfig.xml
MyV4PrintDriverRenderFilter.dll

[DestinationDirs]
DefaultDestDir = 66000

[SourceDisksNames]
1 = %DiskName%,,,""

[SourceDisksFiles]
MyV4PrintDriver.gpd=1
MyV4PrintDriver-manifest.ini=1
MyV4PrintDriverRenderFilter-PipelineConfig.xml=1
MyV4PrintDriverRenderFilter.dll=1

[Strings]
ManufacturerName="Fabrikam"
DiskName="MyV4PrintDriver Installation Disk"
```

### <a name="update-the-driver-files-list"></a>更新**驱动程序文件**列表

1. 在 Visual Studio 的 "解决方案资源管理器中，展开" *MyV4PrinterDriver* "节点。

2. 选择文件 MyV4PrintDriver，并将其拖到 "**驱动程序文件**" 节点。

3. 对 MyV4PrintDriver-manifest 执行相同的操作。

### <a name="add-the-pipeline-config-file-to-the-driver-package"></a>将管道配置文件添加到驱动程序包

1. 在解决方案资源管理器中，右键单击 " *MyV4PrintDriver*项目"，然后单击 "**属性**"。

2. 在 " **MyV4PrintDriver 属性页**" 窗口的左窗格中，展开 "**配置属性**"。

3. 展开 "**驱动程序安装**"，然后单击 "**包文件**"。 在右窗格中执行以下操作：
    - 导航到项目目录。
    - 向下导航到*MyV4PrintDriver Render 筛选器*目录。
    - 选择文件 MyV4PrintDriverRenderFilter-PipelineConfig，并按 "**打开**"。
    - 单击“确定”。

### <a name="add-a-reference-to-the-render-filter-to-the-driver-package"></a>将对呈现筛选器的引用添加到驱动程序包

1. 在 Visual Studio 的 "解决方案资源管理器中，展开" *MyV4PrinterDriver* "节点。

2. 右键单击 "**引用**" 节点 > 选择 "**添加引用**"。

3. 单击 " *MyV4PrintDriver 呈现筛选器*" 复选框，然后单击 **"确定"** 。

### <a name="configure-the-driver-solution-for-debugging-and-deployment"></a>为调试和部署配置驱动程序解决方案

1. 在解决方案资源管理器中，右键单击 " *MyV4PrintDriver*项目"，然后单击 "**属性**"。

2. 在 " **MyV4PrintDriver 属性页**" 窗口的左窗格中，展开 "**配置属性**"。

3. 展开 "**驱动程序安装**"，然后单击 "**部署**"。 在右窗格中执行以下操作：
    - 确保已配置**目标计算机名称**。 如果没有，请单击 "..."并按照**配置设备**向导中的提示设置远程目标计算机。
    - 选中“部署前删除以前的驱动程序版本”。
    - 选择 "**安装/重新安装并验证**"，然后从下拉框中选择 "**默认打印机驱动程序包安装任务**"。
    - 在 "**可选参数**" 字段中键入驱动程序的名称（名称前后没有引号）。
    - 单击“确定”。

### <a name="configure-driver-signing"></a>配置驱动程序签名

1. 在解决方案资源管理器中，右键单击 " *MyV4PrintDriver*项目"，然后单击 "**属性**"。

2. 在 " **MyV4PrintDriver 属性页**" 窗口的左窗格中，展开 "**配置属性**"。

3. 展开 "**驱动程序签名**"，然后单击 "**常规**"。

4. 在右侧窗格中，确认 "**签名模式**" 设置为 "测试签名"。

5. 单击 "**测试证书**"，然后从下拉框中选择 &lt;创建测试证书 ... "&gt;。

6. 单击 " **TimeStampServer**"，然后从下拉框中选择 "Verisign"。

7. 单击“确定”。

### <a name="build-and-deploy-the-driver"></a>生成和部署驱动程序

1. 在解决方案资源管理器中，右键单击 " *MyV4PrintDriver （2个项目）* "，然后单击 "**生成解决方案**"。

2. 生成过程完成后，将自动安装驱动程序。 请确保 "输出" 窗口中没有任何错误。

### <a name="test-the-driver"></a>测试驱动程序

使用即插即用或添加打印机向导创建打印队列。

有关 v4 打印机驱动程序的 INF 文件的详细信息，请参阅[V4 驱动程序 inf](v4-driver-inf.md)。

> [!NOTE]
> 除了上表中的文件，还请注意， *MyV4PrintDriver Render Filter*文件夹已创建。 这是渲染筛选器项目模板，它为构建 XPS 渲染筛选器和 XPS 筛选器管道配置文件提供了良好的基础。 有关 XPS 呈现筛选器的详细信息，请参阅[XPSDrv Render Module](xpsdrv-render-module.md)，若要查看 xps 呈现筛选器的示例，请参阅[Xps 光栅化筛选器服务](https://go.microsoft.com/fwlink/p/?LinkId=617951)示例。
