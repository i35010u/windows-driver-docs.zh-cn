---
title: 查找 ICC 配置文件
description: 查找 ICC 配置文件
ms.assetid: 828b53cd-452a-4c4d-bfbb-45ea674ef49a
keywords:
- 颜色管理 WDK 打印，查找 ICC 配置文件
- ICC 配置文件 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0be3f82b5dc2fe126696bd8262c881330206dea8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568583"
---
# <a name="locating-icc-profiles"></a>查找 ICC 配置文件





启用颜色管理后，GDI 将搜索适当的 ICC 配置文件，使用以下步骤：

1.  如果驱动程序的[打印机接口 DLL](printer-interface-dll.md)提供[ **DrvQueryColorProfile** ](https://msdn.microsoft.com/library/windows/hardware/ff548573)函数，GDI 客户端调用的函数，以便该驱动程序有机会指定配置文件。 如果该函数将返回一个配置文件，则使用它。

2.  如果**DrvQueryColorProfile**不存在或未返回一个配置文件，GDI 搜索已为指定的打印机类型安装的配置文件的颜色目录。 GDI 使用发现解析、 媒体类型和抖色与匹配的第一个配置文件中的 DEVMODE 结构的设置。

3.  如果颜色目录不包含指定的打印机类型与指定的 DEVMODE 内容匹配的任何配置文件，GDI 将使用系统的默认 sRGB 配置文件。

有关详细信息，请参阅[安装 ICC 配置文件](installing-icc-profiles.md)。 Microsoft Windows SDK 文档中可以找到有关 ICC 配置文件的更多信息。

 

 




