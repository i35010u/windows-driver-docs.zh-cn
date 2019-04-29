---
title: 包感知打印驱动程序
description: 包感知打印驱动程序
ms.assetid: f2ab38b9-410c-4dd8-bb81-4a8e0e48317a
keywords:
- 识别包的打印驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54292a6c1d83ab6e21d95a82adcfe60a23863088
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353700"
---
# <a name="package-aware-print-drivers"></a>包感知打印驱动程序


识别包的打印驱动程序支持点和与包打印其 INF 文件中有条目。 这些条目，它们使点和打印以适应其他文件上的打印驱动程序依赖项，可小，且取决于驱动程序包的性质。

-   如果驱动程序包中的文件是唯一的且其他打印驱动程序的包中未列出，请**PackageAware** INF 中的关键字。

-   如果驱动程序包中的文件在其他打印驱动程序的包共享的文件：
    -   将共享的文件移到单独[核心驱动程序](writing-core-drivers.md)。
    -   使用**PackageAware**关键字和**CoreDriverDependencies**关键字来指代此单独的核心驱动程序。 这是为了在各种远程安装方案期间避免文件版本冲突。

本部分包括：

[不共享文件的包感知打印驱动程序](package-aware-print-drivers-that-do-not-share-files.md)

[识别包的共享文件的打印驱动程序](package-aware-print-drivers-that-share-files.md)

 

 




