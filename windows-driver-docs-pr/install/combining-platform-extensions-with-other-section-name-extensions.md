---
title: 将平台扩展与其他节名称扩展相结合
description: 将平台扩展与其他节名称扩展相结合
ms.assetid: ca82ba0f-0d65-47ca-826a-4f78435b1442
keywords:
- INF 文件 WDK 设备安装，平台扩展
- 平台扩展 WDK INF 文件
- 扩展 WDK INF 平台
- 组合平台扩展 WDK INF 文件
- 安装节名称 WDK INF 文件
- 修饰 INF WDK
- 操作系统 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a91dcbbb90dc1b781c070d9d5502958b2328b4cd
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90104894"
---
# <a name="combining-platform-extensions-with-other-section-name-extensions"></a>将平台扩展与其他节名称扩展相结合


包含带有平台扩展的 INF *DDInstall* 部分的 inf 文件也可以包含其他每个设备的部分，例如所需的 <em>DDInstall</em>**。服务** 和可选的 <em>DDInstall</em>**。HW**、 <em>DDInstall</em>**。CoInstallers**、 <em>DDInstall</em>**。LogConfigOverride**和 <em>DDInstall</em>**。接口** 部分。 在跨操作系统和跨平台 INF 文件中，应紧靠在 INF 写入器定义的部分名称之后指定适当的平台扩展 (<em>例如，</em>**ntx86。HW**) 。

如果跨操作系统的 INF 文件包含修饰<em>的安装节名称</em>**. nt** <em>、</em>**ntx86**、**ntia64**或**ntamd64** <em>节，则</em>它还必须具有其他并行修饰的和未修饰的每个<em>设备的节</em>部分的内容。 也就是说，如果 INF 文件同时具有 *安装节名称* 和 <em>安装节名称</em>**nt** 节，则会有一个 *DDInstall*。**硬件** 部分，它还必须具有并行 <em>安装节名称</em>**nt。** 如果设备或驱动程序需要，则 (HW 部分 **。** Windows 2000 和更高版本的 windows) 的硬件部分。

[INF 文件部分和指令](./index.md)部分中的主题显示了**nt**<em>xxx</em>**。** 在相应节引用中作为正式语法语句的一部分的 HW 扩展，如以下示例中所示：

```inf
[install-section-name.HW] | 
[install-section-name.nt.HW] | 
[install-section-name.ntx86.HW] | 
[install-section-name.ntia64.HW] | 
[install-section-name.ntamd64.HW] 
```

这种形式的语法语句表示这些扩展是基本节的有效替代项。 此类型的语句并*不*指示具有<em>安装节名称</em>nt 的任何 INF 文件。**HW**部分还必须包含每个其他特定于平台的<em>安装-名称</em>**。 nt**<em>xxx</em>**。HW**部分。 您可以使用这些扩展的任何子集来指定特定跨平台安装所需的经过修饰的部分。

包含 *安装节名称* 平台扩展的 INF 文件还可以包含平台扩展及其 [**inf SourceDisksNames 部分**](inf-sourcedisksnames-section.md) 和 [**inf SourceDisksFiles 节**](inf-sourcedisksfiles-section.md) 条目，以特定于平台的方式指定安装文件位置。