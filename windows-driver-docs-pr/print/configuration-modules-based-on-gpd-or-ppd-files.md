---
title: 基于 GPD 或 PPD 文件的配置模块
description: 基于 GPD 或 PPD 文件的配置模块
keywords:
- 版本 3 XPS 驱动程序 WDK XPSDrv，GPD 文件
- 版本 3 XPS 驱动程序 WDK XPSDrv、PPD 文件
- GPD 文件 WDK XPSDrv
- PPD 文件 WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c169c8e470c6c386ee63347dac7f49d0e1bc3cc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797603"
---
# <a name="configuration-modules-based-on-gpd-or-ppd-files"></a>基于 GPD 或 PPD 文件的配置模块


对于 Windows Vista，GPD 和 PPD 文件包含特定于 XPSDrv 打印驱动程序的打印架构映射和新条目。 这些更改适用于 GPD 和 PPD 文件，这些文件可用于创建仅限 GPD 或 PPD 的配置模块和 Unidrv 或 Pscript5 打印驱动程序插件的配置模块。

### <a name="xpsdrv-specific-gpd-and-ppd-entries"></a>XPSDrv-Specific GPD 和 PPD 条目

若要使用 GPD 或 PPD 文件为 XPSDrv 打印驱动程序创建版本3打印驱动程序配置模块，必须执行以下操作之一：

-   创建或编辑 GPD 或 PPD 文件。 文件必须包含用于描述打印机支持的功能的配置关键字。 标准 GPD 或 PPD 关键字自动映射到公共打印架构关键字，但默认情况下，非标准关键字映射到专用命名空间。

-   如果创建的是 GPD 文件或 Msxpsinc 文件（如果要创建 PPD 文件），请包含 Msxpsinc. gpd 文件。 这些文件包括以下关键字，它们指示生成的配置文件将是 XPSDrv 打印驱动程序的一部分。

    对于 Msxpsinc gpd，它包含：

    ```cpp
    IsXPSDriver?: TRUE
    ```

    对于 Msxpsinc，它包含：

    ```cpp
    *MSIsXPSDriver: True
    ```

包括 Msxpsinc. gpd 或 Msxpsinc 文件是首选方法，而不是将这些属性添加到 GPD 或 PPD 文件中。 Microsoft 可能会将 XPSDrv 驱动程序的属性添加到相应的包含文件。 如果 Microsoft 将这些新属性添加到包含文件中，并在 GPD 或 PPD 文件中使用包含文件，则不需要编辑打印驱动程序的 GPD 或 PPD 文件。

在 INF 文件中指定的根 GPD 或 PPD 文件 (，作为 `DataFile` 所有 Microsoft Unidrv 或基于 PScript5 驱动程序的 XPSDrv 驱动程序的驱动程序) ，必须包含相应的 Msxpsinc. GPD 或 Msxpsinc 文件。

例如，对于 Model-foo. gpd，包括：

```cpp
*Include: "msxpsinc.gpd"
```

对于 Model-foo，包括：

```cpp
*Include: "msxpinc.ppd"
```

### <a name="print-schema-mapping"></a>打印架构映射

打印架构映射是 Unidrv 和 PScript5 配置模块的一项功能，它将 GPD 和 PPD 关键字转换为其等效的公共打印架构关键字。 默认情况下，所有标准 GPD 和 PPD 关键字都映射到其等效的公共打印架构关键字。 但是，GPD 或 PPD 文件中的非标准关键字默认映射到特定于设备的专用命名空间。 可以通过执行以下一项或两项操作来改进此映射：

-   为非标准关键字指定专用命名空间。

-   使用 GPD 或 PPD 文件中公共打印架构的等效关键字将 GPD 或 PPD 文件中的非标准功能和选项关键字关联起来。 此关联使配置模块可以将 PrintTicket 和 PrintCapabilities 数据生成为公共打印架构功能。

### <a name="gpd-file-example"></a>GPD 文件示例

下面的代码示例演示了一个 GPD 文件，该文件阐释了用于为 XPSDrv 打印驱动程序创建版本3配置模块的项和关键字。

```cpp
*%
*% Copyright (c) 2004 - 2006 Microsoft Corporation
*% All Rights Reserved.
*%
*GPDFileVersion: "1.0"
*GPDSpecVersion: "1.0"
*GPDFileName:    "plugfest.gpd"
*Include:        "StdNames.gpd"
*%
*% Include XPSDrv include file
*%
*Include:        "MSXpsInc.gpd"
*ModelName:      "Microsoft XPS Passthrough Driver Sample"
*MasterUnits:    PAIR(1200, 1200)
*ResourceDLL:    "unires.dll"
*PrinterType:    PAGE
*MaxCopies:      1

*%
*% IHV Private Namespace
*%
*PrintSchemaPrivateNamespaceURI:"https://www.ihv.com/schema/2006"
*%
*% IHV Private Feature
*%
*Feature: IHVStapling { 
*PrintSchemaKeywordMap: "JobStapleAllDocuments"
*Option: Enabled {
  *PrintSchemaKeywordMap: "StapleTopLeft" }
*Option: Disabled {
  *PrintSchemaKeywordMap: "None"  }
}
```

 

 




