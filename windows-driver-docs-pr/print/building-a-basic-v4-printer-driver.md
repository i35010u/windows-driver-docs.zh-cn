---
title: 生成基本的 v4 打印机驱动程序
description: 使用 Microsoft Visual Studio 2017 中的驱动程序开发向导来选择要创建的功能的打印机驱动程序的功能的最小集生成基本 v4 打印机驱动程序。
ms.assetid: 6E50CD69-D385-4724-B6B1-85D42EFFC6F0
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 03e4f77618193c0778250e3a623f34899e3cac1f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63330412"
---
# <a name="building-a-basic-v4-printer-driver"></a>生成基本的 v4 打印机驱动程序

使用 Microsoft Visual Studio 2017 中的驱动程序开发向导来选择要创建的功能的打印机驱动程序的功能的最小集生成基本 v4 打印机驱动程序。

本主题中的说明将专注于构建一个驱动程序所需的步骤，并将说明在向导中提供的许多打印机驱动程序选项。 本主题旨在提供开发 Visual Studio 2017 中的打印机驱动程序时涉及的过程的简介。 中提供了更详细的打印机驱动程序选项看[浏览向导中的驱动程序选项](exploring-the-driver-options-in-the-wizard.md)。

## <a name="instructions"></a>说明

### <a name="select-features-for-the-basic-driver"></a>选择基本驱动程序的功能

1. 在 Visual Studio 中，在主菜单中，单击**文件** &gt; **新建** &gt; **项目**。

2. 在中**新的项目**窗口中，在右上的搜索框中，键入*打印机驱动程序 v4* ，然后按 enter。 此操作将检索名称中包含搜索文本的所有驱动程序模板。

3. 在中间窗格中，选择**打印机驱动程序 V4**。

4. 为您的驱动程序中键入一个名称**名称**字段中，然后依次**确定**。 例如，可以键入*MyV4PrintDriver*。

5. 在中**创建 v4 打印驱动程序向导**下**呈现类型选择的驱动程序：**，单击**V4 打印驱动程序和自定义呈现的筛选器 （仅接受 XPS）**。

6. 保留所有其他选项保留为其默认设置，然后单击**下一步**。

7. 在中**安装程序信息**部分中的向导中，将所有选项保留为其默认设置，然后单击**下一步**。

8. 在中**安装程序信息 （第 2 页）** 部分中的向导中，将所有选项保留为其默认设置，然后单击**下一步**。

Microsoft Visual Studio 使用前面的选择生成的项目文件*MyV4PrintDriver*。

### <a name="verify-the-generated-driver-files"></a>验证生成的驱动程序文件

1. 导航到生成的驱动程序文件的文件夹。 例如，如果名为你的项目*MyV4PrintDriver*，则默认情况下，会将文件保存到以下位置：*我的文档&gt;Visual Studio 2017&gt;项目&gt;MyV4PrintDriver &gt; MyV4PrintDriver*。

2. 验证该文件夹包含以下文件：

    | 文件名                                              | 文件类型                                                  |
    |--------------------------------------------------------|------------------------------------------------------------|
    | MyV4PrintDriver.gpd                                    | 打印机说明文件                                   |
    | MyV4PrintDriver.inf                                    | 安装程序信息文件                                     |
    | MyV4PrintDriver.vcxproj                                | C++项目文件                                           |
    | MyV4PrintDriver.vcxproj.filters                        | C++项目筛选器文件                                   |
    | MyV4PrintDriver-manifest.ini                           | 配置设置文件 （也称为 打印驱动程序清单） |
    | V4PrintDriver-Intellisense.js                          | Intellisense 的 JavaScript 文件                           |
    | V4PrintDriver-Intellisense-Windows8.1.js               | Intellisense 的 JavaScript 文件                           |

请注意，在上表中创建的文件的一个是一个 INF 文件。 请注意，Visual Studio 创建一个具有要完成，以便它可以用于安装驱动程序的主干 INF 文件。

### <a name="create-a-unique-printerdriverid-for-the-driver"></a>创建一个唯一**PrinterDriverID**驱动程序

1. 在 Visual Studio 工具菜单中选择**创建 GUID**。

2. 选择选项**4。注册表格式**然后单击**复制**按钮。

3. 在 Visual Studio 中，在解决方案资源管理器，展开*MyV4PrintDriver*节点。

4. 单击**驱动程序文件**，然后在**属性**窗口中查看的值*唯一标识符*字段。 此值替换为使用生成的 GUID**粘贴**。

### <a name="complete-the-inf-file"></a>完成的 INF 文件

MyV4PrintDriver 项目中应该有一个条目**驱动程序文件**。 打开此和 MyV4PrintDriver.inf 应列出的文件。 打开此文件。

#### <a name="1-update-the-copyright-notice"></a>1.更新版权通知

INF 文件的前两行是驱动程序包的版权声明。

第 1 行包含的年和你的公司名称。 YYYY 的字符替换为当前年份，并替换的字符<Your manufacturer name>与你的公司名称。

第 2 行描述包括制造商名称和设备型号信息驱动程序 INF 的内容。 替换字符&lt;制造商名称&gt;与你的公司名称和替换的字符&lt;打印机型号&gt;使用的打印机驱动程序支持的模型名称。

例如，如果年份是 2017年和贵公司的名称是 Fabrikam，并且打印设备模型是 1234年，将键入以下命令：

```cpp
; Copyright (c) 2017 Fabrikam
; INF file for the Fabrikam 1234 print driver
```

#### <a name="2-verfy-the-version-section-is-correct"></a>2.验证程序**\[版本\]** 部分是否正确

查找行包含**\[版本\]**。

- 检查并确保您看到以下行：

    ```cpp
    **ClassVer**=4.0
    ```
- 检查并确保您看到以下行：

    ```cpp
    **Signature**="$WINDOWS NT$"
    ```

#### <a name="3-configure-the-sourcediskfiles-section"></a>3.配置**\[SourceDiskFiles\]** 部分

查找行包含 **\[SourceDiskFiles\]**。

下面键入以下行：

```cpp
MyV4PrintDriver.gpd=1
MyV4PrintDriver-manifest.ini=1
MyV4PrintDriverRenderFilter-PipelineConfig.xml=1
MyV4PrintDriverRenderFilter.dll=1
```

#### <a name="4-configure-the-driverfiles-section"></a>4.配置**\[DriverFiles\]** 部分

查找行包含 **\[DriverFiles\]**。

下面键入以下行：

```cpp
MyV4PrintDriver.gpd
MyV4PrintDriver-manifest.ini
MyV4PrintDriverRenderFilter-PipelineConfig.xml
MyV4PrintDriverRenderFilter.dll
```

#### <a name="5-configure-the-standardntarch-section"></a>5.配置**\[Standard.NT$ARCH$\]** 部分

查找行包含 **\[Standard.NT$ARCH$\]**。

本部分中引用每个模型 INF 安装的部分。 例如，如果您的打印机的模型为 Fabrikam 1234，然后您键入以下：

```cpp
"Fabrikam 1234"=DriverInstall, USBPRINT\\Fabrikam1234
"Fabrikam 1234"=DriverInstall, WSDPRINT\\Fabrikam1234
```

#### <a name="6-add-printerdriverid-to-the-inf-file"></a>6.添加**PrinterDriverID** INF 文件

在 Visual Studio 中，在解决方案资源管理器，展开*MyV4PrintDriver*节点。

单击**驱动程序文件**，然后在**属性**窗口中查找的值在*唯一标识符*字段。 这是驱动程序 ID (GUID)。 突出显示它，并将其复制

在 INF 文件中，在**\[Standard.NT$ARCH$\]** 部分中，键入以下行：

```cpp
"Fabrikam 1234"=DriverInstall,
```

并将逗号，后面粘贴你在上一步中复制的 GUID。 已完成**\[Standard.NT$ARCH$\]** 部分应如下所示：

```cpp
"Fabrikam 1234"=DriverInstall, {GUID}
"Fabrikam 1234"=DriverInstall, USBPRINT\Fabrikam1234
"Fabrikam 1234"=DriverInstall, WSDPRINT\Fabrikam1234
```

#### <a name="7-configure-the-strings-section"></a>7.配置**\[字符串\]** 部分

查找行包含**\[字符串\]**。

下面将为您的定义*ManufacturerName*字符串。 替换字符&lt;制造商名称&gt;提供目标打印机的制造商的名称，并删除其余行包含你公司的名称;TODO:

例如，如果贵公司的名称是 Fabrikam，您将键入以下命令：

```cpp
ManufacturerName="Fabrikam"
```

#### <a name="8-save-the-inf-file"></a>8.保存 INF 文件。

完成后的 INF 文件，其外观应如下所示：

```cpp
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

1. 在 Visual Studio 中，在解决方案资源管理器，展开*MyV4PrinterDriver*节点。

2. 选择文件 MyV4PrintDriver.gpd 并将其拖到**驱动程序文件**节点。

3. 执行与 MyV4PrintDriver manifest.ini 相同的操作。

### <a name="add-the-pipeline-config-file-to-the-driver-package"></a>将管道配置文件添加到驱动程序包

1. 在解决方案资源管理器，右键单击*MyV4PrintDriver*项目，然后单击**属性**。

2. 在中**MyV4PrintDriver 属性页**窗口中，展开**配置属性**的左窗格中。

3. 展开**驱动程序安装**，然后单击**包文件**。 执行以下操作在右窗格中：
    - 导航到项目目录。
    - 向下导航中，向*MyV4PrintDriver 呈现筛选器*目录。
    - 选择文件 MyV4PrintDriverRenderFilter PipelineConfig.xml，然后按**打开**。
    - 单击 **“确定”**。

### <a name="add-a-reference-to-the-render-filter-to-the-driver-package"></a>将对呈现器筛选器的引用添加到驱动程序包 

1. 在 Visual Studio 中，在解决方案资源管理器，展开*MyV4PrinterDriver*节点。

2. 右键单击**引用**节点-> 选择**添加引用**。

3. 单击复选框*MyV4PrintDriver 呈现筛选器*，然后单击**确定**。

### <a name="configure-the-driver-solution-for-debugging-and-deployment"></a>配置调试和部署的驱动程序解决方案

1. 在解决方案资源管理器，右键单击*MyV4PrintDriver*项目，然后单击**属性**。

2. 在中**MyV4PrintDriver 属性页**窗口中，展开**配置属性**的左窗格中。

3. 展开**驱动程序安装**，然后单击**部署**。 执行以下操作在右窗格中：
    - 絋粄**目标计算机名称**配置。 否则，单击"..."按照中的提示**配置设备**向导来设置远程目标计算机。
    - 选中**部署前删除以前的驱动程序版本**。
    - 选择**安装/重新安装并验证**，然后选择**默认打印机驱动程序包安装任务**从下拉列表框。
    - 键入的名称中的驱动程序**可选参数**（不带任何括住名称） 字段。
    - 单击 **“确定”**。

### <a name="configure-driver-signing"></a>配置驱动程序签名

1. 在解决方案资源管理器，右键单击*MyV4PrintDriver*项目，然后单击**属性**。

2. 在中**MyV4PrintDriver 属性页**窗口中，展开**配置属性**的左窗格中。

3. 展开**驱动程序签名**，然后单击**常规**。

4. 在右窗格中，确认**登录模式**设置为测试登录。

5. 单击**测试证书**，然后选择&lt;创建测试证书...&gt;从下拉列表框。

6. 单击**TimeStampServer**，然后从下拉列表框中选择 Verisign。

7. 单击 **“确定”**。

### <a name="build-and-deploy-the-driver"></a>生成和部署驱动程序

1. 在解决方案资源管理器中右键单击*解决方案 MyV4PrintDriver （2 个项目）*，然后单击**生成解决方案**。

2. 生成过程完成后将自动安装该驱动程序。 请确保在输出窗口中没有任何错误。

### <a name="test-the-driver"></a>测试驱动程序

创建使用即插即用 play 或添加打印机向导的打印队列。

有关 v4 打印机驱动程序的 INF 文件的详细信息，请参阅[V4 驱动程序 INF](v4-driver-inf.md)。

> [!NOTE]
> 除了上表中的文件，请注意*MyV4PrintDriver 呈现筛选器*创建文件夹。 这是呈现筛选器项目模板，用于构建一个 XPS 呈现筛选器和 XPS 筛选器管道配置文件提供良好的基础。 有关 XPS 呈现筛选器的详细信息，请参阅[XPSDrv 呈现模块](xpsdrv-render-module.md)，并查看 XPS 呈现筛选器的示例，请参阅[XPS 光栅化筛选器服务](https://go.microsoft.com/fwlink/p/?LinkId=617951)示例。




