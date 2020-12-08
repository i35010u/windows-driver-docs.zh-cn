---
title: 创建新的设备安装程序类
description: 创建新的设备安装程序类
keywords:
- 设备安装程序类 WDK 设备安装
- 安装类 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5c6dcf5617e7fd16917dc640bb135b6f9124cf9d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827825"
---
# <a name="creating-a-new-device-setup-class"></a>创建新的设备安装程序类





仅当绝对必要时，才应创建新的设备安装程序类。 通常可以将设备分配到 [系统定义的设备安装程序类](/windows-hardware/drivers/install/system-defined-device-setup-classes-reserved-for-system-use)之一。

如果设备满足以下两个条件，则应将其分配给现有的设备安装程序类：

-   设备的安装和配置要求与现有类的要求匹配。

-   你的设备的功能与现有类的功能匹配。

在以下任一情况下，应考虑提供设备共同安装程序：

-   你的设备具有现有设备类型特定 INF 文件不支持的安装要求。

-   设备的安装需要现有类未提供的设备属性页。

如果你的设备提供的功能明显不同于属于现有类的设备提供的功能，则它可能会提供新的设备安装程序类。 但是，绝不要为属于系统提供的某个类的设备创建新的安装程序类。 如果这样做，您将绕过系统提供的类安装程序，并且您的设备将不会正确地集成到系统中。

如果你认为需要新的设备安装程序类，则新类应基于新的设备功能，而不是设备的位置。 例如，支持新总线上的现有设备不需要新的安装程序类。

在创建新的设备安装程序类之前，请联系 Microsoft 了解是否为你的设备类型规划了新系统提供的设备安装程序类

可以使用 INF 文件创建新的设备安装程序类。 除了安装对设备的支持外，INF 文件还可以为设备初始化新的设备安装程序类。 此类 INF 文件有一个 [**Inf ClassInstall32 部分**](inf-classinstall32-section.md)。

 

