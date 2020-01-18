---
title: 开始编写 Hyper-v 可扩展交换机扩展
description: 本部分介绍如何开始编写 Hyper-v 可扩展交换机扩展
ms.assetid: 91C6ED75-1057-4520-8E8E-28817D8F3C81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfcebe72493e14faaa821e4d39e619816146104a
ms.sourcegitcommit: 6d930ed810124ade8e29a617c7abcd399113696f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2020
ms.locfileid: "76256761"
---
# <a name="getting-started-writing-a-hyper-v-extensible-switch-extension"></a>开始编写 Hyper-V 可扩展交换机扩展

Hyper-v 可扩展交换机扩展是一个 NDIS 筛选器或 Windows 筛选平台（WFP）筛选器，可在 Hyper-v 可扩展交换机（也称为 "Hyper-v 虚拟交换机"）中运行。

有3类扩展：捕获、筛选和转发。 它们都可以作为 NDIS 筛选器驱动程序实现。 筛选扩展还可以作为 WFP 筛选器驱动程序实现。

有关驱动程序开发人员的体系结构概述，请参阅[Hyper-v 可扩展交换机概述](overview-of-the-hyper-v-extensible-switch.md)。

若要创建 Hyper-v 可扩展交换机扩展，请执行以下步骤：

1. 了解扩展体系结构和编程模型。
    -   从[Hyper-v 可扩展交换机](hyper-v-extensible-switch.md)开始，阅读有关基于 NDIS 的扩展的联机文档。 捕获、筛选和转发扩展使用标准 NDIS 筛选 API。 已增强 NDIS 接口以提供虚拟交换机和虚拟机的配置、通知和标识。
        [Hyper-v 可扩展交换机功能](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/) [
        
        hyper-v 可扩展交换机](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/index)[的结构和联合](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)
        hyper-v 可扩展交换机[oid](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-oids)
        hyper-v 可扩展交换机状态指示
        hyper-v 可扩展交换机[宏](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-macros)的[状态指示](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-status-indications)
    -   从[使用虚拟交换机筛选](using-virtual-switch-filtering.md)开始，阅读基于 WFP 的扩展的联机文档。
    -   观看以下有关扩展的指导性视频。
        -   [Hyper-v 可扩展交换机上的 TechEd 会话](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2012/VIR307)
        -   [Hyper-v 可扩展交换机，第 I 部分-简介](https://channel9.msdn.com/posts/Hyper-V-Extensible-Switch-Part-I--Introduction)
        -   [Hyper-v 可扩展交换机，第二部分–了解控制路径](https://channel9.msdn.com/posts/Hyper-V-Extensible-Switch-Part-II--Understanding-the-Control-Path)
        -   [Hyper-v 可扩展交换机，第 III 部分-数据路径 for Capture and Filter Extension](https://channel9.msdn.com/posts/Hyper-V-Extensible-Switch-Part-III--The-Ins-and-Outs-of-the-Data-Path-for-Capture-and-Filter-Extensi)
    -   可以使用多个 PowerShell 命令来管理扩展。 这些列在[管理安装的 Hyper-v 可扩展交换机扩展](managing-installed-hyper-v-extensions.md)中列出。

2.  设置开发环境。
    -   安装 Microsoft Visual Studio Professional。
    -   下载并安装[Windows 驱动程序工具包](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)。

3.  研究示例扩展。
    -   下载[NDIS 转发扩展示例](https://go.microsoft.com/fwlink/p/?LinkId=618935)。
    -   下载[WFP 示例](https://go.microsoft.com/fwlink/p/?LinkId=618934)。 这是一个包含 vSwitch 功能的功能原型。

4.  编写扩展。
    -   你可以使用其中一个示例作为起点、移植现有筛选器代码或从头开始编写你的扩展。
    -   如果要开发 NDIS 扩展，则可以使用标准 NDIS INF，其中有一些更改，如[Hyper-v 可扩展交换机扩展的 INF 要求](inf-requirements-for-hyper-v-extensions.md)中所述。

5.  构建扩展并对其进行单元测试。
    -   必须[使用 Visual Studio 生成扩展](https://visualstudio.microsoft.com/vs/)。
    -   你可以通过使用 Visual Studio 编译和运行示例扩展，熟悉扩展生成过程。

6.  了解用于获取扩展签名的 Windows 认证（徽标）过程。
    -   扩展必须通过[Windows 硬件认证包（HCK）](https://docs.microsoft.com/previous-versions/windows/hardware/cert-program/)中的测试。
    -   扩展的要求列在[Windows 硬件认证要求-筛选器驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/cert-program/windows-hardware-certification-requirements---filter-driver)的 VSwitchExtension. ExtensionRequirements 下。

7.  设置 Windows 硬件认证工具包环境。
    -   下载并安装[Windows 硬件认证工具包](https://msdn.microsoft.com/windows/hardware/hh852359)。

8.  为扩展运行 WHCK 测试：
    -   筛选器。
    -   Filter. Security
    -   VSwitchExtension

9.  最终扩展传递 WHCK 认证后，将其提交给 Microsoft。
    -   必须以具有特定格式的 MSI 安装包的形式提交你的扩展，以确保可通过管理包（如[System Center Virtual Machine Manager （SCVMM）2012）](https://docs.microsoft.com/previous-versions/technet-magazine/hh300651(v=msdn.10))跟踪和部署你的扩展。 MSI 格式在[扩展驱动程序 MSI 打包要求](https://docs.microsoft.com/windows-hardware/drivers/network/extension-driver-msi-packaging-requirements)中定义。

10. 在 WindowsServerCatalog.com 上列出你的扩展。
    -   在 WindowsServerCatalog.com 上列出扩展的简短说明。
    -   稍后将提供有关在 WindowsServerCatalog.com 上列出已验证扩展的信息。
