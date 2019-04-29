---
title: 有关客户端呈现的最佳做法
description: 有关客户端呈现的最佳做法
ms.assetid: d05086c1-4e0b-4767-bb1d-7b6d73b1b210
keywords:
- 客户端呈现 WDK 打印的最佳实践
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cca25f0b73b0e12cb770bcb23be33d2f0315af99
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362004"
---
# <a name="best-practices-for-client-side-rendering"></a>有关客户端呈现的最佳做法


编写打印机驱动程序，以便它们可正常处理客户端呈现时，您应该牢记于心以下各项：

-   应为驱动程序包安装打印机驱动程序。

-   打印机驱动程序应使用 SetPrinterData 或 SetPrinterDataEx 函数来存储打印机配置信息。 有关这些函数的详细信息，请参阅 Microsoft Windows SDK 文档。

-   使用自定义打印处理器的打印机驱动程序必须包括处理器的驱动程序包中并确保该点并将数据打印到客户端计算机上加载。

 

 




