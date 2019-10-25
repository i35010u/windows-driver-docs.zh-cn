---
title: NDIS 驱动程序的版本信息要求
description: NDIS 驱动程序的版本信息要求
ms.assetid: a05e7dde-d1f9-458d-8d7b-ead9bb9af7af
keywords:
- NDIS 版本信息 WDK，NDIS 责任
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f10408f8a868f56457826573d5c26b52cec4f385
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842959"
---
# <a name="version-information-requirements-for-ndis-drivers"></a>NDIS 驱动程序的版本信息要求





提供版本信息的 NDIS 结构包含一个**标头**成员，该成员定义为[ **\_对象\_的标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)结构，ndis 驱动程序必须为此类版本信息提供支持。

NDIS 可支持比*当前版本的 ndis*支持更高或更低的 ndis 版本的驱动程序（即，计算机运行的操作系统版本支持的 ndis 版本）。 另外，驱动程序所支持的驱动程序的*已注册 NDIS 版本*（即，在初始化期间驱动程序报告的版本）可能低于驱动程序所支持的最高版本。 例如，NDIS 5.1 驱动程序或 NDIS 6.1 驱动程序可在运行 NDIS 6.0 的操作系统版本上运行。 NDIS 5.1 驱动程序在初始化期间只注册为 NDIS 5.1 驱动程序。 但是，NDIS 6.1 驱动程序必须检查 NDIS 的当前版本，并必须注册为支持可用的最高级别 NDIS 的驱动程序（在本示例中，为 NDIS 6.0）。 有关如何获取当前 NDIS 版本的详细信息，请参阅[获取 Ndis 版本](obtaining-the-ndis-version.md)。

**请注意**  在结构的更高版本中，不需要使用驱动程序来支持所有功能。 例如，微型端口驱动程序可以创建版本2结构并提供适合于版本1结构的值。

 

若要访问具有版本信息的结构中的成员，NDIS 驱动程序必须完成以下过程：

-   在访问结构中的任何成员之前，检查**标头. 修订号**和**标头。**

-   对于较早版本的结构（即，版本号低于与驱动程序支持的 NDIS 版本关联的数字的结构）：
    -   驱动程序必须验证标头的**大小**是否正确。**修订**值。 例如，NDIS\_SIZEOF\_Xxx\_修订版本的值\_1 对于 Xxx\_修订版是正确的1，但对于 Xxx\_\_\_，此值太小。
    -   **标头**的值必须等于或大于 NDIS\_SIZEOF\_XXX\_修订版本\_Nn （其中*Nn*是驱动程序所使用的结构的修订号），驱动程序必须正确地处理结构中的信息适用于该修订版本。
-   对于更高版本的结构（即版本号比驱动程序支持的 NDIS 版本关联的编号更高的结构），驱动程序可以使用结构，就像它是该结构的较旧版本一样。 更高版本的结构始终与较旧的版本兼容。

-   驱动程序必须对已注册的 NDIS 版本的驱动程序使用正确的结构版本。 例如，NDIS 6.1 驱动程序必须通过将[**ndis\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_object_header)结构中的成员设置为指示 NDIS\_卸载\_修订版来在[**ndis\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_offload)结构中报告其卸载功能\_2。 但是，驱动程序不必支持 NDIS\_卸载\_版本\_2 中包含的所有功能。

-   成功处理 OID 集请求的驱动程序必须在从 OID 集请求返回时在[**NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构中设置**SupportedRevision**成员。 **SupportedRevision**成员向发起方通知驱动程序所支持的修订版本。 例如，微型端口驱动程序可以创建 Xxx\_修订版\_2 结构，提供适用于 Xxx\_修订版\_1 结构的值，并使用零填充结构的其余部分。 小型端口驱动程序会在**SupportedRevision**成员中报告 XXX\_修订版\_1。 在这种情况下，可以支持\_修订版\_2 的协议驱动程序将使用支持微型端口驱动程序的 Xxx\_修订版\_1 信息。

-   若要确定基础驱动程序成功处理的信息，发出 OID 请求的过量驱动程序必须在 SupportedRevision 成员中的成员\_中检查\_请求结构中的值，然后再执行 oid 请求返回.

## <a name="related-topics"></a>相关主题


[NDIS 版本概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

 






