---
title: 配置模块基于 GPD 或 PPD 文件
description: 配置模块基于 GPD 或 PPD 文件
ms.assetid: b0aeea58-1c58-475e-8d4a-597778e42a7c
keywords:
- 版本 3 的 XPS 驱动程序 WDK XPSDrv，GPD 文件
- 版本 3 的 XPS 驱动程序 WDK XPSDrv，PPD 文件
- GPD 文件 WDK XPSDrv
- PPD 文件 WDK XPSDrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4cd79dada49ce41896df9ddb766fd63a10b6e478
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519879"
---
# <a name="configuration-modules-based-on-gpd-or-ppd-files"></a>配置模块基于 GPD 或 PPD 文件


适用于 Windows Vista GPD 和 PPD 文件包含打印架构映射和特定于 XPSDrv 的新条目的打印驱动程序。 可用于创建仅 GPD 或仅 PPD 配置模块和配置模块 Unidrv 或 Pscript5 打印驱动程序插件，这些更改适用于 GPD 和 PPD 文件。

### <a name="xpsdrv-specific-gpd-and-ppd-entries"></a>特定于 XPSDrv 的 GPD 和 PPD 条目

若要使用 GPD 或 PPD 文件创建 XPSDrv 打印机驱动程序的版本 3 打印驱动程序配置模块，必须执行下列任一操作：

-   创建或编辑 GPD 或 PPD 文件。 文件必须包含描述打印机支持的功能的配置关键字。 标准 GPD 或 PPD 关键字将自动映射到公共打印架构关键字，但使用了非标准关键字映射到专用的命名空间，默认情况下。

-   如果要创建 GPD 文件或 Msxpsinc.ppd 文件中，如果要创建 PPD 文件，包括 Msxpsinc.gpd 文件。 这些文件包括以下关键字，指示生成的配置文件将在 XPSDrv 打印驱动程序的一部分。

    对于 Msxpsinc.gpd，它包含：

    ```cpp
    IsXPSDriver?: TRUE
    ```

    对于 Msxpsinc.ppd，它包含：

    ```cpp
    *MSIsXPSDriver: True
    ```

包括 Msxpsinc.gpd 或 Msxpsinc.ppd 文件是一种首选的方法，而不是无需将这些属性添加到 GPD 或 PPD 文件。 Microsoft 无法将 XPSDrv 驱动程序的未来属性添加到相应的包含文件。 如果 Microsoft 将新属性添加到包含文件和 GPD 或 PPD 文件中使用包含文件，不需要编辑打印驱动程序 GPD 或 PPD 文件。

根 GPD 或 PPD 文件 (作为驱动程序的 INF 文件中指定`DataFile`) 所有 Microsoft Unidrv 或 PScript5 驱动程序基于 XPSDrv 驱动程序必须包括相应的 Msxpsinc.gpd 或 Msxpsinc.ppd 文件。

例如，对于模型 foo.gpd，包括：

```cpp
*Include: "msxpsinc.gpd"
```

对于模型 foo.ppd，包括：

```cpp
*Include: "msxpinc.ppd"
```

### <a name="print-schema-mapping"></a>打印架构映射

打印架构映射是 Unidrv 和 PScript5 配置模块的功能，它将转换为其等效的公共打印架构关键字 GPD 和 PPD 关键字。 默认情况下，所有标准 GPD 和 PPD 关键字映射到其等效的公共打印架构关键字。 使用了非标准关键字在 GPD 或 PPD 文件中，但是，映射到一个专用的特定于设备的命名空间默认情况下。 可以通过执行一个或两项操作来提高此映射：

-   指定了非标准关键字的专用命名空间。

-   将从公共 GPD 或 PPD 文件中的打印架构及其等效关键字与关联 GPD 或 PPD 文件中使用了非标准功能和选项的关键字。 这种关联，配置模块生成 PrintTicket 和 PrintCapabilities 数据作为公共打印架构功能。

### <a name="gpd-file-example"></a>GPD 文件示例

下面的代码示例演示说明了条目 GPD 文件和关键字为 XPSDrv 创建版本 3 配置模块打印驱动程序。

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
*PrintSchemaPrivateNamespaceURI:"http://www.ihv.com/schema/2006"
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

 

 




