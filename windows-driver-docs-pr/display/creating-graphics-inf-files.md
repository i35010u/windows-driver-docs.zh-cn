---
title: 创建图形 INF 文件
description: 创建图形 INF 文件
ms.assetid: e56d4881-5ad2-41fc-a6fb-bc72c5106361
keywords:
- 显示驱动程序模型 WDK Windows 2000，图形
- Windows 2000 显示器驱动程序模型 WDK，图形
- 视频微型端口驱动程序 WDK Windows 2000，图形
- 显示驱动程序 WDK Windows 2000，图形
- INF 文件 WDK Windows 2000 显示
- graphics INF 文件 WDK Windows 2000 显示
- geninf.exe
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ed1d590e4f89af3c420be0f12ea4cbed1fe28d99
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067332"
---
# <a name="creating-graphics-inf-files"></a>创建图形 INF 文件


## <span id="ddk_creating_graphics_inf_files_gg"></span><span id="DDK_CREATING_GRAPHICS_INF_FILES_GG"></span>


必须使用 INF 文件安装基于 NT 的操作系统显示和视频微型端口驱动程序。 驱动程序开发工具包 (DDK) 提供一种名为 *geninf.exe* 的工具，通过该工具，你可以为显示器和视频微型端口驱动程序生成 INF 文件。

**注意**   *geninf.exe*工具在 Windows 驱动程序工具包 (WDK) 中不可用，这将取代了 DDK。

 

运行 *geninf.exe* 时，它会显示多个对话框，提示您提供信息，例如公司名称和显示驱动程序和视频微型端口驱动程序的名称。 然后*Geninf.exe*从该信息生成 INF 文件。

**注意**   *geninf.exe*生成的文件可能不是完全有效的 INF 文件。 *Geninf.exe* 会生成一个 inf 文件，该文件可能需要为 inf 文件中所述的每个设备添加自定义注册表设置。

 

如果微型端口驱动程序映射的设备内存超过 8 MB，则应手动编辑 INF 文件，使其包括 [Inf GeneralConfigData 部分](inf-generalconfigdata-section.md)中所述的部分和适当的条目。

运行 *geninf.exe*时，请在系统提示选择设备类时选择 "显示"。 在驱动程序安装过程中，系统提供的显示类安装程序会解释标记为 **类 = 显示** 的 INF 文件。 这可确保与视频驱动程序关联的所有注册表项都已正确初始化。

类 **显示** 的 INF 文件只能在系统上安装以下文件：

-   单个微型端口驱动程序

-   单个显示器驱动程序

-   控制面板扩展 Dll

不能从类 **显示**的 INF 文件中安装其他类型的驱动程序或应用程序文件。

### <a name="span-idlimitations_of_geninfexespanspan-idlimitations_of_geninfexespanspan-idlimitations_of_geninfexespanlimitations-of-geninfexe"></a><span id="Limitations_of_geninf.exe"></span><span id="limitations_of_geninf.exe"></span><span id="LIMITATIONS_OF_GENINF.EXE"></span>geninf.exe 的限制

不能使用 *geninf.exe* 生成：

-   支持多个体系结构的 INF 文件。

-   支持 Windows 95/98/Me 或 Windows NT 4.0 或更早版本的 INF 文件。

-   *镜像驱动程序*的 INF 文件。 使用随 *镜像* 示例驱动程序提供的 INF 文件作为模板。 有关更多详细信息，请参阅 [镜像驱动程序 INF 文件](mirror-driver-inf-file.md) 。

-   监视器 INF 文件。 使用名为 *monsamp* 的 inf 作为模板。 有关更多详细信息，请参阅 [监视 INF 文件部分](monitor-inf-file-sections.md) 。

这些示例 INF 文件随 Windows 驱动程序工具包一起附带 (WDK) 。

有关更新示例 INF 文件的详细信息，请参阅 [创建 Inf 文件](../install/overview-of-inf-files.md) 和 [inf 文件部分和指令](https://docs.microsoft.com/windows-hardware/drivers/install/inf-file-sections-and-directives) 。

 

