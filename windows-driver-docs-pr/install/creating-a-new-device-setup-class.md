---
title: 创建新的设备安装程序类
description: 创建新的设备安装程序类
ms.assetid: 3235d1e9-f6f7-4efe-a50c-5ea7a9956e7e
keywords:
- 设备安装程序类 WDK 设备安装
- 安装程序类 WDK 设备安装
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d80bc77f27e8d774e8bf844721cd1f9dcbd15105
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576978"
---
# <a name="creating-a-new-device-setup-class"></a>创建新的设备安装程序类





您只应创建新的设备安装程序类，如果绝对必要。 通常可以将你的设备分配给之一[系统定义的设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff553419)。

如果你的设备满足下列要求，应将其分配给现有的设备安装程序类：

-   你的设备的安装和配置要求相符的现有类。

-   你的设备的功能与现有类相匹配。

在以下任一情况下，应考虑提供的设备的共同安装程序：

-   你的设备有现有的设备特定于类型的 INF 文件中不受支持的安装要求。

-   设备的安装要求设备不提供在现有类的属性页。

如果你的设备提供了通过属于现有类的设备所提供的功能明显不同的功能，可能需要新的设备安装程序类。 但是，必须永远不会创建一个新的安装程序类属于系统提供的类之一的设备。 如果这样做，将绕过系统提供的类安装程序并不会将你的设备正确集成到系统。

如果您认为需要新的设备安装程序类，在新的设备功能，而不是设备的位置应基于您的新类。 例如，支持新总线上的现有设备应该不需要新的安装程序类。

在创建新的设备安装程序类之前, 与 Microsoft 联系以找出你的设备类型是否计划新的系统提供的设备安装程序类

可以通过使用 INF 文件创建新的设备安装程序类。 安装对设备的支持，除了 INF 文件可以初始化新的设备安装程序类的设备。 此类的 INF 文件具有[ **INF ClassInstall32 部分**](inf-classinstall32-section.md)。

 

 





