---
title: 包感知打印驱动程序
description: 包感知打印驱动程序
keywords:
- 包感知打印驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0730b916ce62f91b059821df6bfe2f91e7b2dd4d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807663"
---
# <a name="package-aware-print-drivers"></a>包感知打印驱动程序


包感知打印驱动程序的 INF 文件中有一些条目，这些条目支持使用包的点和打印。 这些条目使点和打印可容纳打印驱动程序在其他文件上的依赖项，这可能很小，并且取决于驱动程序包的性质。

-   如果驱动程序包中的文件是唯一的，且未列在其他打印驱动程序包中，请在 INF 中使用 **PackageAware** 关键字。

-   如果驱动程序包中的文件与其他打印驱动程序包中的文件共享：
    -   将共享文件移动到单独的 [核心驱动程序](writing-core-drivers.md)中。
    -   使用 **PackageAware** 关键字和 **CoreDriverDependencies** 关键字引用此独立的核心驱动程序。 这是为了避免在各种远程安装方案中发生文件版本冲突。

本节包括：

[不共享文件的包感知打印驱动程序](package-aware-print-drivers-that-do-not-share-files.md)

[共享文件的包感知打印驱动程序](package-aware-print-drivers-that-share-files.md)

 

 




