---
title: 编写入门的 HYPER-V 可扩展交换机扩展
description: 本部分介绍如何开始编写的 HYPER-V 可扩展交换机扩展
ms.assetid: 91C6ED75-1057-4520-8E8E-28817D8F3C81
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30f93b3e047839d98d15c1a76859874eedf4d5d0
ms.sourcegitcommit: f663c383886d87ea762e419963ff427500cc5042
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67393402"
---
# <a name="getting-started-writing-a-hyper-v-extensible-switch-extension"></a>开始编写 Hyper-V 可扩展交换机扩展


NDIS 筛选器或 HYPER-V 可扩展交换机 （也称为"HYPER-V 虚拟交换机"） 中运行的 Windows 筛选平台 (WFP) 筛选器，HYPER-V 可扩展交换机扩展。

有 3 个类的扩展： 捕获、 筛选以及转发。 所有这些可作为 NDIS 筛选器驱动程序。 筛选扩展也作为 WFP 筛选器驱动程序实现。

有关驱动程序开发人员的体系结构概述，请参阅[概述的 HYPER-V 可扩展交换机](overview-of-the-hyper-v-extensible-switch.md)。

若要创建的 HYPER-V 可扩展交换机扩展，请执行以下步骤：

1.  了解扩展体系结构和编程模型。
    -   阅读基于 NDIS 的扩展，开头的联机文档[HYPER-V 可扩展交换机](hyper-v-extensible-switch.md)。 捕获、 筛选以及转发扩展使用标准的 NDIS 筛选 API。 NDIS 接口已得到增强，提供配置、 通知和虚拟交换机和虚拟机的标识。
        [HYPER-V 可扩展交换机函数](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)
        [HYPER-V 可扩展交换机枚举](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/index)
        [HYPER-V 可扩展交换机结构和联合](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_netvista/)
        [的 HYPER-V 可扩展交换机 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-oids)
        [HYPER-V 可扩展交换机状态指示](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-status-indications)
        [的 HYPER-V 可扩展交换机宏](https://docs.microsoft.com/windows-hardware/drivers/network/hyper-v-extensible-switch-macros)
    -   阅读基于 WFP 的扩展，开头的联机文档[使用虚拟交换机筛选](using-virtual-switch-filtering.md)。
    -   观看扩展上的以下说明视频。
        -   [TechEd 会话上的 HYPER-V 可扩展交换机](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2012/VIR307)
        -   [HYPER-V 可扩展交换机，第 I 部分 — 简介](https://channel9.msdn.com/posts/Hyper-V-Extensible-Switch-Part-I--Introduction)
        -   [HYPER-V 可扩展交换机，第 ii 部分 — 了解控制路径](https://channel9.msdn.com/posts/Hyper-V-Extensible-Switch-Part-II--Understanding-the-Control-Path)
        -   [HYPER-V 可扩展交换机，第 iii 部分 — 用于捕获和筛选器扩展数据路径的细节](https://channel9.msdn.com/posts/Hyper-V-Extensible-Switch-Part-III--The-Ins-and-Outs-of-the-Data-Path-for-Capture-and-Filter-Extensi)
    -   有多个可用于管理扩展的 PowerShell 命令。 中列出了这些[管理安装的 HYPER-V 可扩展交换机扩展](managing-installed-hyper-v-extensions.md)。

2.  设置开发环境。
    -   安装 Microsoft Visual Studio Professional 2012。
    -   下载并安装[Windows Driver Kit 8](https://developer.microsoft.com/windows/hardware)。

3.  研究的示例扩展插件。
    -   下载[转发扩展插件示例的 NDIS](https://go.microsoft.com/fwlink/p/?LinkId=618935)。
    -   下载[WFP 示例](https://go.microsoft.com/fwlink/p/?LinkId=618934)。 这是包括 vSwitch 功能的正常工作原型。

4.  编写你的扩展。
    -   可以使用其中一个示例作为起点，移植现有筛选器代码，或从头开始编写你的扩展。
    -   如果正在开发的 NDIS 扩展，您可以使用标准的 NDIS INF 带有少量的更改中所述[INF 的 HYPER-V 可扩展交换机扩展的要求](inf-requirements-for-hyper-v-extensions.md)。

5.  构建您的扩展插件和单元测试。
    -   您必须[使用 Visual Studio 生成扩展以](https://msdn.microsoft.com/library/windows/hardware/ff554644.aspx)。
    -   你可以熟悉扩展生成过程使用 Visual Studio 编译和运行的示例扩展插件。

6.  了解有关获取签名的扩展的 Windows 认证 （徽标） 过程。
    -   扩展必须通过在测试[Windows 硬件认证工具包 (HCK)](https://go.microsoft.com/fwlink/p/?LinkId=733613)。
    -   扩展的要求下列出在 Filter.Driver.vSwitchExtension.ExtensionRequirements [Windows 硬件认证要求的筛选器驱动程序](https://docs.microsoft.com/previous-versions/windows/hardware/cert-program/windows-hardware-certification-requirements---filter-driver)。

7.  设置 Windows 硬件认证工具包环境。
    -   下载并安装[Windows 硬件认证工具包](https://msdn.microsoft.com/windows/hardware/hh852359)。

8.  运行扩展 WHCK 测试：
    -   Filter.Driver.Fundamentals
    -   Filter.Driver.Security
    -   Filter.Driver.vSwitchExtension

9.  您最终的扩展插件通过 WHCK 认证后，将其提交给 Microsoft。
    -   您的扩展插件必须提交为具有特定的格式，以确保它可以进行跟踪并部署的管理包，如 MSI 安装程序包[System Center Virtual Machine Manager (SCVMM) 2012年](https://docs.microsoft.com/previous-versions/technet-magazine/hh300651(v=msdn.10))。 中定义的 MSI 格式[扩展驱动程序 MSI 打包要求](https://docs.microsoft.com/windows-hardware/drivers/network/extension-driver-msi-packaging-requirements)。

10. 列出您 WindowsServerCatalog.com 的扩展。
    -   列出您的扩展 WindowsServerCatalog.com 的简短说明。
    -   列出 WindowsServerCatalog.com 上经过认证的扩展的信息将很快可用。

 

 





