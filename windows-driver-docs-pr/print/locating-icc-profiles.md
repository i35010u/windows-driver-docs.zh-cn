---
title: 查找 ICC 配置文件
description: 查找 ICC 配置文件
ms.assetid: 828b53cd-452a-4c4d-bfbb-45ea674ef49a
keywords:
- 颜色管理 WDK 打印，查找 ICC 配置文件
- ICC 配置文件 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 12a2db1c7dcc4e29b07ba9668c14df136a0cdbe4
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842619"
---
# <a name="locating-icc-profiles"></a>查找 ICC 配置文件





启用颜色管理后，GDI 将使用以下步骤搜索相应的 ICC 配置文件：

1.  如果驱动程序的[打印机接口 DLL](printer-interface-dll.md)提供[**DrvQueryColorProfile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvquerycolorprofile)函数，则 GDI 客户端将调用该函数，以使该驱动程序有机会指定配置文件。 如果该函数返回一个配置文件，则使用该配置文件。

2.  如果**DrvQueryColorProfile**不存在或未返回配置文件，则 GDI 将在颜色目录中搜索已为指定打印机类型安装的配置文件。 GDI 使用它找到的第一个配置文件，该配置文件与 DEVMODE 结构中的分辨率、媒体类型和抖动设置相匹配。

3.  如果颜色目录不包含与指定的 DEVMODE 内容匹配的指定打印机类型的任何配置文件，则 GDI 将使用系统的默认 sRGB 配置文件。

有关详细信息，请参阅[安装 ICC 配置文件](installing-icc-profiles.md)。 有关 ICC 配置文件的其他信息可在 Microsoft Windows SDK 文档中找到。

 

 




