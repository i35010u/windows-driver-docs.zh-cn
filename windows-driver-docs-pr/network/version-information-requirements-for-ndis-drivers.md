---
title: NDIS 驱动程序的版本信息要求
description: NDIS 驱动程序的版本信息要求
keywords:
- NDIS 版本信息 WDK，NDIS 责任
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7c7a0963ea1916c7386a0627b2f552cdbed4ab9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839413"
---
# <a name="version-information-requirements-for-ndis-drivers"></a>NDIS 驱动程序的版本信息要求





提供版本信息的 NDIS 结构包含一个 **标头** 成员，该成员定义为 [**NDIS \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header) 结构，ndis 驱动程序必须为此类版本信息提供支持。

NDIS 可以支持比 *当前版本的 ndis* 支持更高或更低版本的驱动程序， (即计算机运行) 的操作系统版本支持的 ndis 版本。 此外， *已注册的 NDIS 版本* (即，驱动程序在初始化) 过程中报告的版本可能低于驱动程序支持的最高版本。 例如，NDIS 5.1 驱动程序或 NDIS 6.1 驱动程序可在运行 NDIS 6.0 的操作系统版本上运行。 NDIS 5.1 驱动程序在初始化期间只注册为 NDIS 5.1 驱动程序。 但是，NDIS 6.1 驱动程序必须检查 NDIS 的当前版本，并必须注册为支持在此示例中 (的最高级别 NDIS 的驱动程序，NDIS 6.0) 。 有关如何获取当前 NDIS 版本的详细信息，请参阅 [获取 Ndis 版本](obtaining-the-ndis-version.md)。

**注意**  在结构的更高版本中，不需要使用驱动程序来支持所有功能。 例如，微型端口驱动程序可以创建版本2结构并提供适合于版本1结构的值。

 

若要访问具有版本信息的结构中的成员，NDIS 驱动程序必须完成以下过程：

-   在访问结构中的任何成员之前，检查 **标头. 修订号** 和 **标头。**

-   对于较早版本的结构 (即，其修订号低于与驱动程序支持的 NDIS 版本关联的数字的结构) ：
    -   驱动程序必须验证标头的 **大小** 是否正确。 **修订** 值。 例如，NDIS \_ SIZEOF \_ xxx 版本1的值 \_ \_ 是正确的 xxx \_ 版本1， \_ 但它对于 xxx 版本2而言太 \_ 小 \_ 。
    -   **标头** 的值必须等于或大于 NDIS \_ SIZEOF \_ Xxx \_ REVISION \_ Nn (，其中 *Nn* 是驱动程序使用的结构的修订号) 并且驱动程序必须正确地处理结构中的信息，这是适合于该修订版本的。
-   对于更高版本的结构 (也就是说，版本号比驱动程序) 支持的 NDIS 版本关联的数字更高的结构，驱动程序可以使用结构，就像它是该结构的较旧版本一样。 更高版本的结构始终与较旧的版本兼容。

-   驱动程序必须对已注册的 NDIS 版本的驱动程序使用正确的结构版本。 例如，NDIS 6.1 驱动程序必须通过将 [**ndis \_ 对象 \_ 标头**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)结构中的成员设置为指示 ndis 卸载修订版本2，在 [**ndis \_ 卸载**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构中报告其卸载功能 \_ \_ \_ 。 但是，驱动程序不必支持 NDIS \_ 卸载 \_ 修订版本2中包含的所有功能 \_ 。

-   成功处理 OID 集请求的驱动程序必须在从 OID 集请求返回时在 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中设置 **SupportedRevision** 成员。 **SupportedRevision** 成员向发起方通知驱动程序所支持的修订版本。 例如，微型端口驱动程序可以创建 Xxx \_ 版本 \_ 2 结构，提供适合于 Xxx \_ 版本1结构的值 \_ ，并使用零填充结构的其余部分。 微型端口驱动程序会 \_ \_ 在 **SupportedRevision** 成员中报告 Xxx 版本1。 在这种情况下，可以支持 Xxx 版本2的协议驱动程序 \_ \_ 将使用 \_ \_ 微型端口驱动程序支持的 xxx 版本1信息。

-   若要确定基础驱动程序成功处理的信息，发出 OID 请求的过量驱动程序必须在 **SupportedRevision** \_ \_ OID 请求返回后，在 NDIS OID 请求结构中检查 SupportedRevision 成员中的值。

## <a name="related-topics"></a>相关主题


[NDIS 版本概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

