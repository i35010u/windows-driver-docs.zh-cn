---
title: 将平台扩展与其他节名称扩展相结合
description: 将平台扩展与其他节名称扩展相结合
ms.assetid: ca82ba0f-0d65-47ca-826a-4f78435b1442
keywords:
- INF 文件 WDK 设备安装，平台扩展
- 平台扩展 WDK INF 文件
- 扩展 WDK INF 平台
- 组合平台扩展 WDK INF 文件
- 安装的部分名称 WDK INF 文件
- 修饰的 INF WDK
- 操作系统 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b4234541fcb785fe0112bc8e0386682d3dfe1879
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361179"
---
# <a name="combining-platform-extensions-with-other-section-name-extensions"></a>将平台扩展与其他节名称扩展相结合


INF 文件，其中包含 INF *DDInstall*平台扩展包含的部分也可以包含其他每个设备的部分中，例如，required <em>DDInstall</em>**。服务**和可选<em>DDInstall</em>**。HW**， <em>DDInstall</em>**。共同安装程序**， <em>DDInstall</em>**。LogConfigOverride**，并<em>DDInstall</em>**。接口**部分。 在跨操作系统系统和跨平台 INF 文件中，您应指定相应的平台扩展紧跟 INF 编写器定义的节名称 (例如，<em>安装的部分名称</em>**.ntx86。HW**)。

如果跨操作系统系统 INF 文件包含修饰<em>安装的部分名称</em>**.nt**，<em>安装的部分名称</em>**.ntx86**， <em>安装的部分名称</em>**.ntia64**，或<em>安装的部分名称</em>**.ntamd64**的部分中，它必须还具有其他并行修饰和未修饰每个设备部分。 也就是说，如果 INF 文件同时*安装部分名称*和<em>安装部分名称</em>**.nt**部分，并且它具有*DDInstall*。**HW**部分中，它必须还具有一种并行<em>安装的部分名称</em>**.nt。HW**部分 (如果该设备或驱动程序要求 **。HW**部分，了解 Windows 2000 和更高版本的 Windows)。

中的主题[INF 文件的部分和指令](inf-file-sections-and-directives.md)本节演示**nt**<em>xxx</em>**。HW**作为相应部分中的正式语法语句的一部分的扩展引用，此类，如以下示例所示：

**\[**<em>安装的部分名称</em>**。HW\]** |
**\[**<em>安装部分名称</em>**.nt。HW\]** |
**\[**<em>安装部分名称</em>**.ntx86。HW\]** |
**\[**<em>安装部分名称</em>**.ntia64。HW\]** |
**\[**<em>安装部分名称</em>**.ntamd64。HW\] **正式语法语句指示这些扩展是基本部分的有效替代方法。 此类型的语句执行*不*指示的具有任何 INF 文件<em>安装部分名称</em>**.nt。HW**部分中还必须包括每个其他特定于平台的<em>安装的部分名称</em>**.nt**<em>xxx</em>**。HW**部分。 这些扩展的任何子集可用于指定特定的跨平台安装所需的修饰的部分。

INF 文件，其中包含*安装的部分名称*平台扩展，还可以使用的平台扩展其[ **INF SourceDisksNames 部分**](inf-sourcedisksnames-section.md)和[ **INF SourceDisksFiles 部分**](inf-sourcedisksfiles-section.md)条目，以特定于平台的方式指定安装文件位置。

 

 





