---
title: 网络设备的标准化 INF 关键字
description: 网络设备的标准化 INF 关键字
ms.assetid: F79AFB63-D404-4A5C-9515-82FFEB667048
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5311923887ac2e43954e74a3d38f89136f70e38d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216548"
---
# <a name="standardized-inf-keywords-for-network-devices"></a>网络设备的标准化 INF 关键字





本部分提供有关在注册表中出现并在 INF 文件中指定的标准化关键字的信息。 Ndis 6.0 和更高版本的 NDIS 在网络设备中支持微型端口驱动程序的标准化关键字。

标准化关键字提供：

-   最终用户的标准化用户界面属性。

-   家庭网络用户和大规模企业可以轻松地配置包含多个硬件制造商设备的网络的能力。

-   能够以编程方式测试所有高级网络设备功能。

对于无连接 NDIS 6.0 和更高版本的微型端口驱动程序，以下标准 INF 关键字是必需的：

-   **\*IfType**

-   **\*MediaType**

-   **\*PhysicalMediaType**

如果驱动程序的 INF 文件中缺少必需的关键字，NDIS 不会调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数。

如果以下两个条件均为 true，则 NDIS 6.0 和更高的微型端口驱动程序需要标准化关键字：

-   INF 设置必须在用户界面的 " **高级** 属性" 页中公开。

-   设备完全支持指定的属性。

**注意**   标准化关键字是可选的，但建议用于 NDIS 5.1 和更早的 NDIS 微型端口驱动程序。

 

此部分指定在用户界面中公开的 INF 关键字。 但是，微型端口驱动程序必须在初始化过程中读取注册表设置，以确定当前的配置设置。

在 INF 文件中，这些关键字的定义与 "高级属性" 页的其他定义放置在一起。 有关高级属性的详细信息，请参阅 [指定高级属性页的配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

所有标准化关键字名称都以星号开头 (**\***) 。 此命名约定使你可以轻松地将标准化名称与非标准名称区分开来。

用户界面中公开了三种类型的标准化关键字数据：

<a href="" id="enum"></a>枚举  
可从 " **高级** 属性" 页的下拉菜单中显示的列表中选择的值。

<a href="" id="int"></a>整形  
可以编辑的数值。

<a href="" id="edit"></a>编辑  
可以编辑的文本值。

以下主题包括所有网络技术共有的标准化关键字的说明：

[枚举关键字](enumeration-keywords.md)

[可编辑的关键字](keywords-that-can-be-edited.md)

[不在用户界面中显示的关键字](keywords-not-displayed-in-the-user-interface.md)

此外，以下主题中介绍了特定于网络技术的标准化关键字：

[筛选器驱动程序的 INF 文件设置](inf-file-settings-for-filter-drivers.md)

[NDKPI 的 INF 要求](inf-requirements-for-ndkpi.md)

[MB 微型端口驱动程序 INF 要求](mb-miniport-driver-inf-requirements.md)

[标头数据拆分的标准化 INF 关键字](standardized-inf-keywords-for-header-data-split.md)

[用于 NDIS 服务质量的标准 INF 关键字 (QoS) ](standardized-inf-keywords-for-ndis-qos.md)

[NDIS 选择性挂起的标准化 INF 关键字](standardized-inf-keywords-for-ndis-selective-suspend.md)

[NVGRE 任务卸载的标准化 INF 关键字](standardized-inf-keywords-for-nvgre-task-offload.md)

[数据包合并的标准化 INF 关键字](standardized-inf-keywords-for-packet-coalescing.md)

[电源管理的标准化 INF 关键字](standardized-inf-keywords-for-power-management.md)

[RSC 的标准化 INF 关键字](standardized-inf-keywords-for-rsc.md)

[RSS 的标准化 INF 关键字](standardized-inf-keywords-for-rss.md)

[单个根 i/o 虚拟化的标准化 INF 关键字 (SR-IOV) ](standardized-inf-keywords-for-sr-iov.md)

[适用于虚拟机队列 (VMQ 的标准化 INF 关键字) ](standardized-inf-keywords-for-vmq.md)

 

