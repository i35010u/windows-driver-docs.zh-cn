---
title: 创建图形 INF 文件
description: 创建图形 INF 文件
ms.assetid: e56d4881-5ad2-41fc-a6fb-bc72c5106361
keywords:
- 显示器驱动程序模型 WDK Windows 2000 中，图形
- Windows 2000 显示器驱动程序模型 WDK，图形
- 微型端口驱动程序 WDK Windows 2000 中，图形
- 显示驱动程序 WDK Windows 2000 中，图形
- INF 文件 WDK Windows 2000 显示
- INF 文件 WDK Windows 2000 的图形显示
- geninf.exe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 673e56e9911f39df38ccb27556f18eb07ec82fe2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370185"
---
# <a name="creating-graphics-inf-files"></a>创建图形 INF 文件


## <span id="ddk_creating_graphics_inf_files_gg"></span><span id="DDK_CREATING_GRAPHICS_INF_FILES_GG"></span>


必须使用 INF 文件安装在基于 NT 的操作系统显示和视频的微型端口驱动程序。 驱动程序开发工具包 (DDK) 提供了一个工具，称为*geninf.exe* ，可以生成用于显示和视频微型端口驱动程序的 INF 文件。

**请注意**   *geninf.exe*工具不可用在 Windows Driver Kit (WDK)，它将替换 DDK。

 

当*geninf.exe*是运行时，显示对话框，提示您输入信息，例如公司名称和显示器驱动程序和视频的微型端口驱动程序的名称的数字。 *Geninf.exe*然后生成一个 INF 文件中的信息。

**请注意**  生成的文件*geninf.exe*可能不是完全有效的 INF 文件。 *Geninf.exe*生成将可能需要添加自定义注册表设置每个设备 INF 文件中所述的 INF 文件。

 

如果微型端口驱动程序映射多个 8 MB 中的设备内存，则应手动编辑要包括的一节的 INF 文件和合适的条目中所述[INF GeneralConfigData 部分](inf-generalconfigdata-section.md)。

在运行时*geninf.exe*，选择"显示"当系统提示你选择的设备类。 INF 文件标记为**类 = 显示**在驱动程序安装过程中系统提供显示类安装程序将解释。 这可确保与视频驱动程序相关联的所有注册表项已正确都初始化。

类的一个 INF 文件**显示**可以安装仅在系统上的以下文件：

-   单个微型端口驱动程序

-   单个显示器驱动程序

-   控件面板扩展 Dll

可以从类的 INF 文件安装任何其他类型的驱动程序或应用程序文件**显示**。

### <a name="span-idlimitationsofgeninfexespanspan-idlimitationsofgeninfexespanspan-idlimitationsofgeninfexespanlimitations-of-geninfexe"></a><span id="Limitations_of_geninf.exe"></span><span id="limitations_of_geninf.exe"></span><span id="LIMITATIONS_OF_GENINF.EXE"></span>Geninf.exe 的限制

不能使用*geninf.exe*生成：

-   支持多个体系结构一个 INF 文件。

-   支持 Windows 95/98/Me 或 Windows NT 4.0 或以前版本的 INF 文件。

-   一个*镜像驱动程序*INF 文件。 使用随提供的 INF 文件*镜像*作为模板的示例驱动程序。 请参阅[镜像驱动程序 INF 文件](mirror-driver-inf-file.md)的更多详细信息。

-   监视器 INF 文件。 使用名为 INF *monsamp.inf*作为模板。 请参阅[监视器 INF 文件部分](monitor-inf-file-sections.md)的更多详细信息。

这些示例 INF 文件同时传送使用 Windows Driver Kit (WDK)。

请参阅[创建一个 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/overview-of-inf-files)并[INF 文件的部分和指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives)更新示例 INF 文件时的详细信息。

 

 





