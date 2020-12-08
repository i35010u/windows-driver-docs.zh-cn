---
title: WDTF 体系结构和概述
description: 了解 Microsoft Windows 设备测试框架如何 (WDTF) 使你能够创建、管理、重复使用和扩展以设备为中心的基于方案的自动测试。
keywords:
- Windows 设备测试框架 WDK
- WDTF WDK
- 脚本 WDK WDTF
- Windows 设备测试框架 WDK，关于 WDTF
- WDTF WDK，关于 Windows 设备测试框架
- 测试脚本 WDK WDTF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4e2dae5e8e615d0c45f6b289a40b98ab4b7af76e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785341"
---
# <a name="wdtf-architecture-and-overview"></a>WDTF 体系结构和概述


使用 Microsoft Windows 设备测试框架 (WDTF)，你可以创建、管理、重用和扩展以设备为中心、基于方案的自动化测试。

下图显示了在非常高的级别创建方案的典型 WDTF 模型。

![说明在极高级别创建方案的典型 wdtf 模型的关系图 ](images/wdtf-scenariomodel.gif)

测试脚本通过组件对象模型 (COM) 接口使用 WDTF 对象。 你可以使用任何支持 COM 自动化的编程语言来编写这些方案。 本文档提供 VBScript、c + + 和 JScript 中的代码示例。

此外，还可以通过驱动测试管理器 (DTM) 使用某些 WDTF 示例，而无需任何其他编码。

**注意**  DTM 是 [Windows 硬件认证工具包的一部分 (HCK)](/windows-hardware/test/hlk/) 和 Microsoft Windows 徽标工具包 (WLK) 。 在 DTM 中运行基于 WDTF 的测试时，将为你安装 WDTF。

 

上图显示了用于创建基于组件的方案的模型，该模型使你能够专注于一组设备（而不是单个设备）的通用功能。 即使许多设备需要对某些接口进行特殊实现，它们也非常容易添加。 当方案涉及到使用新功能时，可以 [添加](extending-the-framework.md) 一个将该功能包装到 WDTF 的简单 COM 自动化接口。

## <a name="in-this-section"></a>在本节中


-   [WDTF 体系结构](wdtf-architecture.md)
-   [扩展框架](extending-the-framework.md)

 

