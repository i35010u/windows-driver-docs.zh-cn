---
title: WDTF 体系结构和概述
description: 了解 Microsoft Windows 设备测试框架 (WDTF) 如何使您能够创建、 管理、 重用和扩展以设备为中心的基于方案的自动的测试。
ms.assetid: 7e7660ec-1f17-4987-82c0-f62cca3a99b9
keywords:
- Windows 设备测试框架 WDK
- WDTF WDK
- 脚本 WDK WDTF
- 测试框架 WDK WDTF 有关 Windows 设备
- WDTF WDK，有关 Windows 设备测试框架
- 测试脚本 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 50b80966ab530d1d58eff813e3087390638b7667
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392704"
---
# <a name="wdtf-architecture-and-overview"></a>WDTF 体系结构和概述


使用 Microsoft Windows 设备测试框架 (WDTF)，你可以创建、管理、重用和扩展以设备为中心、基于方案的自动化测试。

下图显示了用于在非常高级别创建方案的典型 WDTF 模型。

![说明用于在非常高的级别创建方案的典型 wdtf 模型关系图 ](images/wdtf-scenariomodel.gif)

测试脚本使用 WDTF 对象可通过组件对象模型 (COM) 接口。 可以使用支持 COM 自动化编写这些方案的任何编程语言。 本文档提供了代码示例在 VBScript 中， C++，和 JScript。

此外，您可以使用一些 WDTF 示例通过驱动程序测试管理器 (DTM) 而无需任何额外的编码。

**请注意**  DTM 属于[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?linkid=254893)和 Microsoft Windows Logo Kit (WLK)。 运行时基于 WDTF 的测试中 DTM，WDTF 是为你安装。

 

以上图所示的模型创建的基于组件的方案，可让你专注于一组而不是各个设备的设备的常见功能。 即使很多设备需要特殊的实现对于某些这些接口，它们很容易添加。 当一个方案涉及使用一项新功能时，你可以[添加](extending-the-framework.md)简单 COM 自动化接口包装到 WDTF 该功能。

## <a name="in-this-section"></a>本节内容


-   [WDTF 体系结构](wdtf-architecture.md)
-   [扩展框架](extending-the-framework.md)

 

 




