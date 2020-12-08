---
title: 复制 INF 文件
description: 复制 INF 文件
keywords:
- INF 文件 WDK 设备安装，复制
- 正在复制 INF 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f7b71c1a44a04c57a7421c53f49b36930bbb3433
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782937"
---
# <a name="copying-inf-files"></a>复制 INF 文件





有时需要在设备安装过程中复制 INF 文件，以便 Windows 可以在不重复显示用户提示的情况下找到它们。 例如，多功能设备的基本 INF 文件可能会复制设备的各个功能的 INF 文件，以便 Windows 在每次安装设备的功能时都可以查找这些 INF 文件，而不会提示用户。

若要复制 INF 文件，INF 文件可以使用 [**Inf CopyINF 指令**](inf-copyinf-directive.md)。

这样做将：

-   安装适当的目录文件（如果存在）以及 INF 文件。

-   为 INF 文件指定唯一的名称，使其不会覆盖任何其他 INF 文件，而不会被其他 INF 文件覆盖。

-   保留要从中复制设备文件的源介质的路径。

-   确保与 Windows 未来版本的兼容性。

安装软件绝不能将 INF 文件直接复制到系统的 *% SystemRoot%/inf* 目录中。 使用本部分中未介绍的技术复制 INF 文件会使驱动程序的数字签名无效。

 

 





