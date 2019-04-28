---
title: 网络设备的标准化 INF 关键字
description: 网络设备的标准化 INF 关键字
ms.assetid: F79AFB63-D404-4A5C-9515-82FFEB667048
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d55125e09c24d6b12248b4802e6a992ee71543a2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63345962"
---
# <a name="standardized-inf-keywords-for-network-devices"></a>网络设备的标准化 INF 关键字





本部分提供有关出现在注册表和 INF 文件中指定的标准化关键字的信息。 NDIS 6.0 和更高版本的 NDIS 网络设备中的微型端口驱动程序支持标准化的关键字。

提供了标准化的关键字：

-   标准化为最终用户的用户界面属性。

-   若要轻松地配置网络，包括来自多个硬件制造商生产的设备为家庭网络用户和大型企业功能。

-   能够以编程方式对其进行测试所有高级网络设备功能。

以下标准 INF 关键字是强制性的无连接的 NDIS 6.0 和更高版本的微型端口驱动程序：

-   **\*IfType**

-   **\*MediaType**

-   **\*PhysicalMediaType**

如果从驱动程序的 INF 文件缺少必需的关键字，NDIS 不会调用微型端口驱动程序[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数。

如果以下条件都成立，标准化的关键字是 NDIS 6.0 和更高版本的微型端口驱动程序所必需的：

-   INF 设置必须以公开**高级**用户界面的属性页。

-   设备完全支持指定的属性。

**请注意**  标准化关键字是可选的但建议在 NDIS 5.1 及更早的 NDIS 微型端口驱动程序。

 

本部分中指定的用户界面中公开的 INF 关键字。 但是，微型端口驱动程序必须在初始化，以确定当前的配置设置期间读取的注册表设置。

在 INF 文件中，这些关键字的定义位于高级的属性页的其他定义。 有关高级属性的详细信息，请参阅[的高级属性页指定配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

所有标准化关键字名称开始，有一个星号 (* *\\* * *)。 此命名约定，可轻松地非标准名称区分开的标准化的名称。

有三种类型的用户界面中公开的标准化的关键字数据：

<a href="" id="enum"></a>枚举  
可从下拉列表中的菜单中显示的列表中选择的值**高级**属性页。

<a href="" id="int"></a>Int  
您可以编辑的数字值。

<a href="" id="edit"></a>编辑  
您可以编辑的文本值。

下面的主题包括标准化关键字所共有的所有网络技术的说明：

[枚举关键字](enumeration-keywords.md)

[可编辑的关键字](keywords-that-can-be-edited.md)

[用户界面中未显示的关键字](keywords-not-displayed-in-the-user-interface.md)

此外，特定于网络技术的标准化的关键字所述的以下主题：

[筛选器驱动程序的 INF 文件设置](inf-file-settings-for-filter-drivers.md)

[NDKPI INF 要求](inf-requirements-for-ndkpi.md)

[MB 微型端口驱动程序 INF 要求](mb-miniport-driver-inf-requirements.md)

[标头数据拆分的标准化的 INF 关键字](standardized-inf-keywords-for-header-data-split.md)

[NDIS 服务质量 (QoS) 的标准化的 INF 关键字](standardized-inf-keywords-for-ndis-qos.md)

[标准化的 INF 关键字 ndis 选择性挂起](standardized-inf-keywords-for-ndis-selective-suspend.md)

[NVGRE 任务卸载的标准化的 INF 关键字](standardized-inf-keywords-for-nvgre-task-offload.md)

[数据包合并的标准化的 INF 关键字](standardized-inf-keywords-for-packet-coalescing.md)

[电源管理的标准化的 INF 关键字](standardized-inf-keywords-for-power-management.md)

[RSC 的标准化的 INF 关键字](standardized-inf-keywords-for-rsc.md)

[RSS 的标准化的 INF 关键字](standardized-inf-keywords-for-rss.md)

[单根 I/O 虚拟化 (SR-IOV) 的标准化的 INF 关键字](standardized-inf-keywords-for-sr-iov.md)

[虚拟机队列 (VMQ) 的标准化的 INF 关键字](standardized-inf-keywords-for-vmq.md)

 

 





