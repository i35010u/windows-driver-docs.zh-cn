---
title: 指示对 NDIS QoS 操作参数的更改
description: 指示对 NDIS QoS 操作参数的更改
ms.assetid: BAE99C83-2732-4216-BC49-23F541AA3F10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1fae81558d4bc033af10ae31453ae371db0b4646
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405225"
---
# <a name="indicating-changes-to-the-operational-ndis-qos-parameters"></a>指示对 NDIS QoS 操作参数的更改


支持 NDIS 服务质量 (QoS) 问题的微型端口驱动程序[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状态指示驱动程序的操作的 NDIS QoS 参数解析时在第一次或更高版本更改时。 微型端口驱动程序使用这些操作的参数，以执行 QoS 数据包传输配置网络适配器。

微型端口驱动程序必须遵循这些准则以颁发[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状态指示：

-   微型端口驱动程序必须发出[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状态指示后它解析其操作的 NDIS QoS 参数并使用它们配置网络适配器。

    **请注意**如果注册表中的专用本地 NDIS QoS 参数设置微型端口驱动程序，则该驱动程序必须发出[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)期间或之后调用的状态指示[ *MiniportInitializeEx*](https://msdn.microsoft.com/library/windows/hardware/ff559389)。 在这种情况下，该驱动程序初始化[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)带有其专有的本地 NDIS QoS 参数设置的结构。

    有关驱动程序如何解决其操作的 NDIS QoS 参数设置的详细信息，请参阅[解析操作的 NDIS QoS 参数](resolving-operational-ndis-qos-parameters.md)。

-   此初始状态指示后, 微型端口驱动程序应发出[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状态指示其操作的 NDIS QoS 参数已发生更改时。 例如，可以在以下情况下更改操作的 NDIS QoS 参数：

    -   操作的 NDIS QoS 参数将由于更改而更改为本地的 NDIS QoS 参数。 这些参数可以通过 OID 方法请求的更改[OID\_QOS\_参数](https://msdn.microsoft.com/library/windows/hardware/hh451835)或管理应用程序开发的独立硬件供应商 (IHV)。

    -   由于与远程对等方的 QoS 设置冲突更改的操作的 NDIS QoS 参数。

        微型端口驱动程序将使用 IEEE 802.1Qaz 要发现的远程对等方的 QoS 参数的数据中心桥接交换 (DCBX) 协议。 如果启用了愿意状态 DCBX，驱动程序必须按照为 DCBX 状态引擎定义的过程解决其 QoS 参数和远程对等方的 QoS 参数之间的差异。 有关此状态引擎的详细信息，请参阅 IEEE 802.1Qaz 草案标准。

        有关本地 DCBX 愿意状态，请参阅[管理本地 DCBX 愿意状态](managing-the-local-dcbx-willing-state.md)。

    **请注意**当微型端口驱动程序收到本地或远程 NDIS QoS 参数时，它不应颁发[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状态指示，指示是否发生不了任何更改操作的 NDIS QoS 参数。 如果该驱动程序进行这种不必要的状态指示，NDIS 不可能将指示传递给过量驱动程序。

-   微型端口驱动程序应发出[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状态指示当需要对其重写用于解析操作的 NDIS QoS 参数的本地 NDIS QoS 参数。

    微型端口驱动程序通知 NDIS 和基础驱动程序，它已被重写本地的 NDIS QoS 参数通过发出[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状态指示。 对于此类型的指示，该驱动程序必须设置适当**NDIS\_QOS\_参数\_*Xxx*\_CHANGED**中标志**标志**的成员[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构，以指定重写本地的 NDIS QoS 参数的原因。

    有关如何微型端口驱动程序管理的本地 QoS 参数的详细信息，请参阅[设置本地 NDIS QoS 参数](setting-local-ndis-qos-parameters.md)。

    微型端口驱动程序如何解析其操作的 QoS 参数的详细信息，请参阅[解析操作的 NDIS QoS 参数](resolving-operational-ndis-qos-parameters.md)。

**请注意**微型端口驱动程序必须发出[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状态指示如果其 NDIS QoS 功能当前通过启用 **\*QOS**关键字标准化 INF 关键字。 有关详细信息，请参阅[NDIS QoS 的标准化 INF 关键字](standardized-inf-keywords-for-ndis-qos.md)。

## <a name="guidelines-for-issuing-the-ndisstatusqosoperationalparameterschange-status-indication"></a>用于颁发 NDIS 准则\_状态\_QOS\_OPERATIONAL\_参数\_更改状态指示


微型端口驱动程序按照以下步骤时它会发出[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状态指示：

1.  微型端口驱动程序分配的缓冲区，则足以包含以下信息：

    -   [ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构，其中包含的 NDIS QoS 配置设置以及全局操作参数的 NDIS QoS 通信类。

    -   一个数组[ **NDIS\_QOS\_分类\_元素**](https://msdn.microsoft.com/library/windows/hardware/hh451631)结构。 每个这些结构指定流量分类定义的数据包数据模式 (*条件*) 和关联的 IEEE 802.1p 优先级级别 (*操作*)。 如果网络适配器中传输，找到模式或*出口*，与条件匹配的数据包，它为数据包分配关联的优先级级别。 适配器也适用于数据包优先级级别的其它 NDIS QoS 策略。

2.  微型端口初始化[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构与操作的 NDIS QoS 参数。 该驱动程序必须提供一整套的操作参数，包括不可能的网络适配器配置这些参数。

    当微型端口驱动程序初始化**标头**成员，它会设置**类型**的成员**标头**到 NDIS\_对象\_类型\_QOS\_参数。 微型端口驱动程序集**修订**的成员**标头**到 NDIS\_QOS\_参数\_修订\_1 和**大小**成员添加到 NDIS\_SIZEOF\_QOS\_参数\_修订\_1。

    微型端口驱动程序设置的相应**NDIS\_QOS\_参数\_*Xxx*\_CHANGED**标志中**标志**成员的对应成员包含自微型端口 driverissued 以来已更改的数据如果[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状态指示。

    **请注意**设置**NDIS\_QOS\_参数\_*Xxx*\_CHANGED**标志是可选的。 NDIS 始终假定的成员[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)是最新的即使它们没有改变的上一个[ **NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439810)状态指示。

    有关如何设置的详细信息**标志**成员，请参阅[设置的指导原则**标志**成员](#guidelines-for-setting-the-flags-member)。

3.  微型端口驱动程序初始化[ **NDIS\_QOS\_分类\_元素**](https://msdn.microsoft.com/library/windows/hardware/hh451631)操作的 NDIS QoS 中的每个流量分类的结构参数。 驱动程序会添加这些元素的末尾[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)缓冲区中的结构。

    **请注意**微型端口驱动程序不能设置 NDIS\_QOS\_分类\_已强制执行\_BY\_中的微型端口标志**标志**的任何成员[**NDIS\_QOS\_分类\_元素**](https://msdn.microsoft.com/library/windows/hardware/hh451631)结构。

    驱动程序集**NumClassificationElements**的成员[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构的数量数组中的分类元素。 驱动程序集**FirstClassificationElementOffset**成员添加到第一个元素的字节偏移量开始的缓冲区。 驱动程序还设置**ClassificationElementSize**成员添加到数组中的每个元素的长度，以字节为单位。

    **请注意**NDIS 6.30 从开始，必须设置微型端口驱动程序**ClassificationElementSize**成员添加到`sizeof(NDIS_QOS_CLASSIFICATION_ELEMENT`)。

4.  微型端口驱动程序初始化[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构如下所示的状态指示：

    -   **StatusCode**成员必须设置为 NDIS\_状态\_QOS\_OPERATIONAL\_参数\_更改。

    -   **StatusBuffer**成员必须设置为指向包含操作的 NDIS QoS 参数的缓冲区的指针。

    -   **StatusBufferSize**成员必须设置为缓冲区的长度，以字节为单位。

5.  微型端口驱动程序问题的状态指示通过调用[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)。 该驱动程序必须传递一个指向[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构*StatusIndication*参数。

## <a name="guidelines-for-setting-the-flags-member"></a>设置标记成员指南

微型端口驱动程序设置以下标志**标志**的成员[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构，以指定的已配置或更改网络适配器上操作的 NDIS QoS 参数：

<a href="" id="ndis-qos-parameters-ets-configured"></a>**NDIS\_QOS\_参数\_ETS\_已配置**  
如果设置此标志，微型端口驱动程序已配置的网络适配器具有以下成员中包含的 ETS 参数：

-   **NumTrafficClasses**

-   **PriorityAssignmentTable**

-   **TcBandwidthAssignmentTable**

-   **TsaAssignmentTable**

**请注意**微型端口驱动程序必须支持 ETS 才能支持 DCB 的 NDIS QoS。 但是，此标志的设置不指定网络适配器是否支持 ETS。 相反，此标志的设置指定仅在网络适配器都配置了 ETS 参数。

<a href="" id="ndis-qos-parameters-ets-changed"></a>**NDIS\_QOS\_参数\_ETS\_已更改**  
如果设置此标志中的以下成员已更改一个或多个 ETS 参数：

-   **NumTrafficClasses**

-   **PriorityAssignmentTable**

-   **TcBandwidthAssignmentTable**

-   **TsaAssignmentTable**

<a href="" id="ndis-qos-parameters-pfc-configured"></a>**NDIS\_QOS\_参数\_PFC\_已配置**  
如果设置此标志，微型端口驱动程序已与中包含的 PFC 设置配置网络适配器**PfcEnable**成员。

**请注意**微型端口驱动程序必须支持 PFC 才能支持 DCB 的 NDIS QoS。 此标志的设置不会指定网络适配器是否支持 PFC。 相反，此标志的设置指定仅在网络适配器上是否启用 PFC 参数。



<a href="" id="ndis-qos-parameters-pfc-changed"></a>**NDIS\_QOS\_参数\_PFC\_已更改**  
如果设置此标志中, 已更改一个或多个 PFC 设置**PfcEnable**成员。

<a href="" id="ndis-qos-parameters-classification-configured"></a>**NDIS\_QOS\_参数\_分类\_已配置**  
如果设置此标志，微型端口驱动程序已与 QoS 流量分类配置的网络适配器中的以下成员指定的参数：

-   **NumClassificationElements**

-   **ClassificationElementSize**

-   **FirstClassificationElementOffset**

<a href="" id="ndis-qos-parameters-classification-changed"></a>**NDIS\_QOS\_参数\_分类\_已更改**  
如果设置此标志中的以下成员已更改一个或多个 QoS 流量分类参数：

-   **NumClassificationElements**

-   **ClassificationElementSize**

-   **FirstClassificationElementOffset**

**请注意** **NDIS\_QOS\_参数\_*Xxx*\_配置**必须设置标志，如果[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构包含 NDIS QoS 参数设置。 微型端口驱动程序必须设置这些标志而不考虑是否设置已发生更改。 但是，该驱动程序必须设置**NDIS\_QOS\_参数\_*Xxx*\_CHANGED**仅针对已更改这些设置的标志。