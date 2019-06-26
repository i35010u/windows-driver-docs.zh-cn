---
title: NDIS 驱动程序的版本信息要求
description: NDIS 驱动程序的版本信息要求
ms.assetid: a05e7dde-d1f9-458d-8d7b-ead9bb9af7af
keywords:
- NDIS 版本信息 WDK，NDIS 职责
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f25bcdf8db765cfb8ae3b64a9ff7e9c016d0e7ed
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384358"
---
# <a name="version-information-requirements-for-ndis-drivers"></a>NDIS 驱动程序的版本信息要求





提供版本信息的 NDIS 结构具有**标头**定义为成员[ **NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header)结构和的 NDIS 驱动程序必须提供有关此类版本信息的支持。

NDIS 可以支持支持与的 NDIS 版本更高版本或更低的驱动程序*当前版本的 NDIS* （即计算机正在运行的操作系统版本支持的 NDIS 版本）。 此外*注册的 NDIS 版本*（即，驱动程序报告在初始化过程的版本） 的驱动程序可以是低于该驱动程序支持的最高版本。 例如，NDIS 5.1 驱动程序或 NDIS 6.1 驱动程序可以运行 NDIS 6.0 的操作系统版本上运行。 NDIS 5.1 驱动程序只需将注册为 NDIS 5.1 驱动程序在初始化过程。 但是，NDIS 6.1 驱动程序必须检查当前的 NDIS 版本，并且必须注册为支持的最高级别 （在此示例中，NDIS 6.0） 可用的 NDIS 驱动程序。 有关如何获取最新的 NDIS 版本的详细信息，请参阅[获取 NDIS 版本](obtaining-the-ndis-version.md)。

**请注意**  驱动程序不需要支持一种结构的更高版本的修订版本中的所有功能。 例如，微型端口驱动程序可以创建版本 2 结构并提供适用于版本 1 结构的值。

 

若要访问具有版本信息的结构中的成员，NDIS 驱动程序必须完成以下过程：

-   检查**Header.Revision**并**Header.Size**才能访问该结构中的任何成员的成员。

-   对于早期版本结构 （即，具有比与该驱动程序支持的 NDIS 版本相关联的数目较低的修订号的结构）：
    -   该驱动程序必须验证**Header.Size**值是否适合**Header.Revision**值。 例如，值为 NDIS\_SIZEOF\_Xxx\_修订\_1 是正确的 Xxx\_修订\_1，但它是太小，Xxx\_修订\_2。
    -   **Header.Size**值必须等于或大于 NDIS\_SIZEOF\_Xxx\_修订\_Nn (其中*Nn*是的修订号使用该驱动程序的结构） 和驱动程序必须正确处理中的结构，以根据该修订版本的信息。
-   对于更高版本结构 （即，比与该驱动程序支持的 NDIS 版本相关联的数目的更高版本的修订号的结构），该驱动程序可以使用结构，就好像不较旧版本的结构。 更高版本的结构始终是使用早期版本兼容。

-   驱动程序必须使用已注册的 NDIS 版本的驱动程序的正确版本的一种结构。 例如，NDIS 6.1 驱动程序必须报告在其卸载功能[ **NDIS\_卸载**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_offload)中设置成员的结构[ **NDIS\_对象\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_object_header)结构，以指示 NDIS\_卸载\_修订\_2。 但是，该驱动程序不需要支持所有功能所包含的 NDIS\_卸载\_修订\_2。

-   已成功处理的 OID 集请求的驱动程序必须设置**SupportedRevision**中的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)在从 OID 集请求返回的结构。 **SupportedRevision**成员会通知驱动程序支持的修订版本的请求的发起程序。 例如，微型端口驱动程序可以创建 Xxx\_修订\_2 结构，提供适用于 Xxx 的值\_修订\_1 结构和填充了零结构的其余部分。 微型端口驱动程序会报告 Xxx\_修订\_中的 1 **SupportedRevision**成员。 在此情况下，一个协议驱动程序，可支持 Xxx\_修订\_2 将使用 Xxx\_修订\_1 微型端口驱动程序支持的信息。

-   若要确定哪些信息已成功处理由基础驱动程序，过量发出 OID 请求的驱动程序必须检查的值**SupportedRevision**成员在 NDIS\_OID\_请求OID 请求返回的结构。

## <a name="related-topics"></a>相关主题


[NDIS 版本的概述](overview-of-ndis-versions.md)

[指定 NDIS 版本信息](specifying-ndis-version-information.md)

 

 






