---
title: 指示对远程 NDIS QoS 参数的更改
description: 指示对远程 NDIS QoS 参数的更改
ms.assetid: E09EBF25-96B6-417F-9538-D0BEBE5B9E19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03f5b0d9184551e83da99acfae59de2b859cbfc4
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405220"
---
# <a name="indicating-changes-to-the-remote-ndis-qos-parameters"></a>指示对远程 NDIS QoS 参数的更改


支持 NDIS 服务质量 (QoS) 问题的微型端口驱动程序[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态指示其远程 NDIS QoS 参数既接收来自对等方第一次或更高版本更改时。 微型端口驱动程序将从通过 IEEE 802.1Qaz 远程对等方接收这些 QoS 参数的数据中心桥接交换 (DCBX) 协议。

微型端口驱动程序必须遵循这些准则以颁发[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态指示：

-   如果微型端口驱动程序尚未收到来自远程对等方 DCBX 帧，它必须不颁发[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态指示。

-   微型端口驱动程序必须发出[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)后其状态指示首先从远程对等方收到的 QoS 设置。

    **请注意**微型端口驱动程序必须发出此状态指示，如果网络适配器从对等方收到远程 QoS 参数设置之前设置驱动程序的本地 QoS 参数。 有关详细信息，请参阅[设置本地 NDIS QoS 参数](setting-local-ndis-qos-parameters.md)。

-   在此初始状态指示后, 微型端口驱动程序应只能颁发[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态指示在确定远程对等方上的 QoS 设置中的更改时。

    **请注意**微型端口驱动程序不应颁发[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态指示，指示是否不已对远程 NDIS QoS 参数的任何更改。 如果该驱动程序会使这种类型的状态指示，NDIS 不可能将指示传递给过量驱动程序。

**请注意**微型端口驱动程序必须发出[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)如果其 NDIS QoS 功能当前已启用的状态指示。 从 Windows Server 2012 开始，这些指示允许系统管理员查看 NDIS QoS 和无论是否安装了 Microsoft DCB 服务器功能的数据中心桥接 (DCB) 设置。



## <a name="guidelines-for-issuing-the-ndisstatusqosremoteparameterschange-status-indication"></a>用于颁发 NDIS 准则\_状态\_QOS\_远程\_参数\_更改状态指示


微型端口驱动程序按照以下步骤时它会发出[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态指示：

1.  微型端口驱动程序分配的缓冲区，则足以包含以下信息：

    -   [ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构，其中包含的 NDIS QoS 配置设置以及全局操作参数的 NDIS QoS 通信类。

    -   一个数组[ **NDIS\_QOS\_分类\_元素**](https://msdn.microsoft.com/library/windows/hardware/hh451631)结构。 每个这些结构指定流量分类定义的数据包数据模式 (*条件*) 和关联的 IEEE 802.1p 优先级级别 (*操作*)。 如果网络适配器中传输，找到模式或*出口*，与条件匹配的数据包，它为数据包分配关联的优先级级别。 适配器也适用于数据包优先级级别的其它 NDIS QoS 策略。

2.  微型端口初始化[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构与远程 NDIS QoS 参数。 该驱动程序必须提供一整套的远程接收从远程对等方所发送的 DCBX 帧的参数。

    当微型端口驱动程序初始化**标头**成员，它会设置**类型**的成员**标头**到 NDIS\_对象\_类型\_QOS\_参数。 微型端口驱动程序集**修订**的成员**标头**到 NDIS\_QOS\_参数\_修订\_1 和**大小**成员添加到 NDIS\_SIZEOF\_QOS\_参数\_修订\_1。

    微型端口驱动程序设置的相应**NDIS\_QOS\_参数\_*Xxx*\_CHANGED**相应成员包含的数据时标志自以前颁发的微型端口驱动程序以来已更改[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态指示。

    **请注意**设置这些**NDIS\_QOS\_参数\_*Xxx*\_CHANGED**标志是可选的。 NDIS 始终假定的成员[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)即使它们没有改变的上一个指定[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态指示。

    微型端口驱动程序集**标志**成员，才能指定中包含的数据的状态信息[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构成员。

    例如，微型端口驱动程序设置的相应**NDIS\_QOS\_参数\_*Xxx*\_CHANGED**标志中**标志**其中包含的数据自以前颁发的微型端口驱动程序以来已更改这些成员的成员[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态指示。

    有关如何设置的详细信息**标志**成员，请参阅[设置的指导原则**标志**成员](#guidelines-for-setting-the-flags-member)。

3.  微型端口驱动程序初始化[ **NDIS\_QOS\_分类\_元素**](https://msdn.microsoft.com/library/windows/hardware/hh451631)远程 NDIS QoS 中的每个流量分类的结构参数。 驱动程序会添加这些元素的末尾[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)缓冲区中的结构。

    **请注意**微型端口驱动程序不能设置 NDIS\_QOS\_分类\_已强制执行\_BY\_中的微型端口标志**标志**的任何成员[**NDIS\_QOS\_分类\_元素**](https://msdn.microsoft.com/library/windows/hardware/hh451631)结构。

    驱动程序集**NumClassificationElements**的成员[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构的数量数组中的分类元素。 驱动程序集**FirstClassificationElementOffset**成员添加到第一个元素的字节偏移量开始的缓冲区。 驱动程序还设置**ClassificationElementSize**成员添加到数组中的每个元素的长度，以字节为单位。

    **请注意**NDIS 6.30 从开始，必须设置微型端口驱动程序**ClassificationElementSize**成员添加到`sizeof(NDIS_QOS_CLASSIFICATION_ELEMENT`)。

4.  微型端口驱动程序初始化[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构如下所示的状态指示：

    -   **StatusCode**成员必须设置为 NDIS\_状态\_QOS\_远程\_参数\_更改。

    -   **StatusBuffer**成员必须设置为指向包含远程 NDIS QoS 参数的缓冲区的指针。

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

**请注意** **NDIS\_QOS\_参数\_*Xxx*\_配置**必须设置标志，如果[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构包含 NDIS QoS 参数设置。 微型端口驱动程序必须设置这些标志而不考虑是否设置已发生更改。 但是，该驱动程序必须仅设置**NDIS\_QOS\_参数\_*Xxx*\_CHANGED**针对已更改这些设置的标志。

## <a name="guidelines-for-indicating-invalid-remote-ndis-qos-parameters"></a>用于指示无效的远程 NDIS QoS 参数的指导原则


微型端口驱动程序必须使其远程 QoS 参数无效，如果满足以下条件：

-   远程 QoS 参数的过期的生存时间 (TTL) 值。

    **请注意**DCBX 结转 IEEE 802.1AB 中指定的链接层发现协议 (LLDP) 协议的 2005 标准。 LLDP 帧始终包含 TTL 字段。

-   TTL 值过期之前，另一个数据链接对等方将发送 DCBX 帧。 此方案称为*多对等方*条件。 DCBX 需要微型端口驱动程序维护只有一组从单个数据链接对等方接收到的远程 QoS 参数。

    出现多对等情况时，微型端口驱动程序必须使所有远程的 QoS 参数无效直到接收到的 DCBX 帧的所有过期 TTL 值。

当微型端口驱动程序使其远程 NDIS QoS 参数时，它必须执行以下步骤时它会发出[ **NDIS\_状态\_QOS\_远程\_参数\_更改**](https://msdn.microsoft.com/library/windows/hardware/hh439812)状态指示：

1.  微型端口驱动程序未报告任何有效的远程 NDIS QoS 参数，因为它首先必须填充[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)用零的结构。

    当微型端口驱动程序初始化**标头**此结构的成员，它会设置**类型**的成员**标头**到 NDIS\_对象\_类型\_QOS\_参数。 微型端口驱动程序集**修订**的成员**标头**到 NDIS\_QOS\_参数\_修订\_1 和**大小**成员添加到 NDIS\_SIZEOF\_QOS\_参数\_修订\_1。

    微型端口驱动程序设置的相应**NDIS\_QOS\_参数\_*Xxx*\_CHANGED**标志中**标志**成员。

2.  微型端口驱动程序初始化[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构如下所示的状态指示：

    -   **StatusCode**成员必须设置为 NDIS\_状态\_QOS\_远程\_参数\_更改。

    -   **StatusBuffer**成员必须设置为的地址[ **NDIS\_QOS\_参数**](https://msdn.microsoft.com/library/windows/hardware/hh451640)结构。

    -   **StatusBufferSize**成员必须设置为`sizeof(NDIS_QOS_PARAMETERS)`。

3.  微型端口驱动程序问题的状态指示通过调用[ **NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600)。 该驱动程序必须传递一个指向[ **NDIS\_状态\_指示**](https://msdn.microsoft.com/library/windows/hardware/ff567373)结构*StatusIndication*参数。