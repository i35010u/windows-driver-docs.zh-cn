---
title: 指示对远程 NDIS QoS 参数的更改
description: 指示对远程 NDIS QoS 参数的更改
ms.assetid: E09EBF25-96B6-417F-9538-D0BEBE5B9E19
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bfab3b63dc9b9720d8ba659ec8eaf33702334688
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824721"
---
# <a name="indicating-changes-to-the-remote-ndis-qos-parameters"></a>指示对远程 NDIS QoS 参数的更改


支持 NDIS 服务质量（QoS）的微型端口驱动程序会在[ **\_QoS\_远程\_参数时发出 ndis\_状态，\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)在对等方收到其远程 NDIS QoS 参数时，更改状态指示第一次或以后更改。 微型端口驱动程序通过 IEEE 802.1 Qaz 数据中心桥接交换（DCBX）协议从远程对等机接收这些 QoS 参数。

微型端口驱动程序必须遵循以下指导原则，使[**NDIS\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)状态指示：

-   如果微型端口驱动程序尚未收到来自远程对等方的 DCBX 帧，则它不能[ **\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)状态指示。

-   小型端口驱动程序必须在从远程对等节点首次接收到 QoS 设置后，将[**NDIS\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)状态指示。

    **注意** 如果在设置驱动程序的本地 QoS 参数之前，网络适配器接收到对等方的远程 QoS 参数设置，则微型端口驱动程序必须发出此状态指示。 有关详细信息，请参阅[设置本地 NDIS QoS 参数](setting-local-ndis-qos-parameters.md)。

-   在此初始状态指示后，微型端口驱动程序只应[ **\_QOS\_远程\_\_参数时发出 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)，这会确定远程对等.

    **注意** 如果没有对远程 NDIS QoS 参数的更改，微型端口驱动程序不应将[**NDIS\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)状态指示。 如果驱动程序确实会导致此类状态指示，NDIS 可能不会将该指示传递到过量驱动程序。

**注意** 如果当前已启用了其 NDIS QoS 功能，微型端口驱动程序必须发出[**ndis\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)状态指示。 从 Windows Server 2012 开始，这些指示允许系统管理员查看 NDIS QoS 和数据中心桥接（DCB）设置，无论是否安装了 Microsoft DCB 服务器功能。



## <a name="guidelines-for-issuing-the-ndis_status_qos_remote_parameters_change-status-indication"></a>有关将 NDIS\_状态\_QOS\_远程\_参数的准则\_更改状态指示


小型端口驱动程序在[ **\_QOS\_远程\_参数发出 NDIS\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)时遵循这些步骤，\_更改状态指示：

1.  微型端口驱动程序分配一个足够大的缓冲区，以包含以下内容：

    -   [**Ndis\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构，其中包含 ndis qos 配置设置，以及 ndis qos 通信类的全局操作参数。

    -   一组[**NDIS\_QOS\_分类\_元素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)结构。 其中每个结构都指定了由数据包数据模式（*条件*）和关联的 IEEE 802.1 p 优先级（*操作*）定义的流量分类。 如果网络适配器在传输或*传出*数据包中找到与条件匹配的模式，则它会将关联的优先级分配给数据包。 该适配器还会将其他 NDIS QoS 策略应用到基于优先级别的数据包。

2.  小型端口通过远程 NDIS QoS 参数初始化[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构。 驱动程序必须提供从远程对等方发送的 DCBX 帧接收的完整远程参数集。

    当微型端口驱动程序初始化**标头**成员时，它会将**标头**的**类型**成员设置为 NDIS\_对象\_类型\_QOS\_参数。 微型端口驱动程序将**标头**的**修订**成员设置为 NDIS\_QOS\_参数\_修订版本\_1，将**Size**成员设置为 ndis\_\_qos\_\_\_1。

    小型端口驱动程序将相应的**NDIS\_QOS\_参数\_*XXX*\_更改**的标志（如果相应成员包含自微型端口驱动程序先前颁发了 NDIS 后发生了更改的数据） [ **\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)状态指示。

    **注意**  将这些**NDIS\_QOS\_参数\_*XXX*\_更改**的标志是可选的。 NDIS 始终假定指定了[**ndis\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)的成员，即使它们未更改为以前的[**NDIS\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)状态指示。

    微型端口驱动程序将**Flags**成员设置为指定[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构成员中包含的数据的状态信息。

    例如，微型端口驱动程序将相应的**NDIS\_QOS\_参数\_*Xxx*\_** 在包含自微型端口驱动程序后已更改的数据的成员的**flags**成员中更改的标志之前已将[**NDIS\_状态\_QOS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)状态指示。

    有关如何设置**标志**成员的详细信息，请参阅[设置**标志**成员的准则](#guidelines-for-setting-the-flags-member)。

3.  微型端口驱动程序通过远程 NDIS QoS 参数中的每个通信分类初始化[**NDIS\_QOS\_分类\_元素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)结构。 驱动程序将这些元素添加到缓冲区末尾[ **\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构。

    **注意** 微型端口驱动程序不得将 NDIS\_QOS\_分类\_强制实施\_，\_[**qos\_分类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)\_的元素结构的**标志**成员中\_微型端口标志。

    驱动程序将[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的**NumClassificationElements**成员设置为数组中分类元素的数目。 驱动程序将**FirstClassificationElementOffset**成员设置为缓冲区开头的第一个元素的字节偏移量。 驱动程序还将**ClassificationElementSize**成员设置为数组中每个元素的长度（以字节为单位）。

    **注意** 从 NDIS 6.30 开始，微型端口驱动程序必须将**ClassificationElementSize**成员设置为 `sizeof(NDIS_QOS_CLASSIFICATION_ELEMENT`）。

4.  微型端口驱动程序通过以下方式初始化状态指示的[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构：

    -   必须将**StatusCode**成员设置为 NDIS\_状态\_QOS\_远程\_参数\_更改。

    -   **StatusBuffer**成员必须设置为指向包含远程 NDIS QoS 参数的缓冲区的指针。

    -   **StatusBufferSize**成员必须设置为缓冲区的长度（以字节为单位）。

5.  微型端口驱动程序通过调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)发出状态指示。 驱动程序必须向*StatusIndication*参数传递指向[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的指针。

## <a name="guidelines-for-setting-the-flags-member"></a>有关设置标志成员的准则

微型端口驱动程序在[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的**flags**成员中设置以下标志，以指定在网络适配器上配置或更改了哪些操作 NDIS QOS 参数：

<a href="" id="ndis-qos-parameters-ets-configured"></a>**NDIS\_QOS\_参数\_配置的 ETS\_**  
如果设置了此标志，则微型端口驱动程序已将网络适配器配置为具有以下成员中包含的 ETS 参数：

-   **NumTrafficClasses**

-   **PriorityAssignmentTable**

-   **TcBandwidthAssignmentTable**

-   **TsaAssignmentTable**

**注意** 小型端口驱动程序必须支持 ETS，以便支持 DCB 的 NDIS QoS。 但是，此标志的设置未指定网络适配器是否支持 ETS。 相反，此标志的设置仅指定是否在网络适配器上配置 ETS 参数。

<a href="" id="ndis-qos-parameters-ets-changed"></a>**NDIS\_QOS\_参数\_ETS\_更改**  
如果设置此标志，则下列成员中的一个或多个 ETS 参数已更改：

-   **NumTrafficClasses**

-   **PriorityAssignmentTable**

-   **TcBandwidthAssignmentTable**

-   **TsaAssignmentTable**

<a href="" id="ndis-qos-parameters-pfc-configured"></a>**NDIS\_QOS\_参数\_配置的 PFC\_**  
如果设置此标志，微型端口驱动程序已将网络适配器配置为包含在**PfcEnable**成员中的 PFC 设置。

**注意** 小型端口驱动程序必须支持 PFC，以便支持 DCB 的 NDIS QoS。 此标志的设置未指定网络适配器是否支持 PFC。 相反，此标志的设置仅指定是否在网络适配器上启用 PFC 参数。

<a href="" id="ndis-qos-parameters-pfc-changed"></a>**NDIS\_QOS\_参数\_PFC\_更改**  
如果设置此标志，则**PfcEnable**成员中已更改一个或多个 PFC 设置。

<a href="" id="ndis-qos-parameters-classification-configured"></a>**已配置\_\_分类\_的 NDIS\_QOS 参数**  
如果设置此标志，微型端口驱动程序已将网络适配器配置为具有以下成员中指定的 QoS 流量分类参数：

-   **NumClassificationElements**

-   **ClassificationElementSize**

-   **FirstClassificationElementOffset**

<a href="" id="ndis-qos-parameters-classification-changed"></a> **\_\_分类\_更改了 NDIS\_QOS 参数**  
如果设置此标志，则下列成员中的一个或多个 QoS 流量分类参数已更改：

-   **NumClassificationElements**

-   **ClassificationElementSize**

-   **FirstClassificationElementOffset**

**注意** 如果[**ndis\_qos\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构包含 ndis QOS 参数设置，则必须设置 **\_qos\_参数\_*Xxx*\_配置**的标志。 无论设置是否已更改，微型端口驱动程序都必须设置这些标志。 但是，驱动程序必须仅将 NDIS\_QOS\_参数设置为已更改的设置的 **\_*XXX*\_更改**标志。

## <a name="guidelines-for-indicating-invalid-remote-ndis-qos-parameters"></a>指示无效远程 NDIS QoS 参数的准则


如果满足以下条件，微型端口驱动程序必须使其远程 QoS 参数失效：

-   远程 QoS 参数的生存时间（TTL）值过期。

    **注意** DCBX 按 IEEE 802.1 AB-2005 标准中指定的方式进行传输。 LLDP 帧始终包含 TTL 字段。

-   其他数据链接对等端在 TTL 值过期之前发送 DCBX 帧。 此方案称为*多对等*条件。 DCBX 要求微型端口驱动程序只保留一组从单个数据链路对等端接收的远程 QoS 参数。

    发生多对等情况时，微型端口驱动程序必须使所有远程 QoS 参数失效，直至所有接收到的 DCBX 帧的 TTL 值过期。

当微型端口驱动程序使其远程 NDIS QoS 参数失效时，必须按照以下步骤发出[**NDIS\_状态\_QoS\_远程\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-remote-parameters-change)状态指示：

1.  由于微型端口驱动程序未报告任何有效的远程 NDIS QoS 参数，因此必须先使用零填充[**NDIS\_QoS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构。

    当微型端口驱动程序初始化此结构的**标头**成员时，它会将**标头**的**类型**成员设置为 NDIS\_对象\_类型\_QOS\_参数。 微型端口驱动程序将**标头**的**修订**成员设置为 NDIS\_QOS\_参数\_修订版本\_1，将**Size**成员设置为 ndis\_\_qos\_\_\_1。

    微型端口驱动程序将相应的**NDIS\_QOS\_参数\_*Xxx*\_** 在**flags**成员中更改的标志。

2.  微型端口驱动程序通过以下方式初始化状态指示的[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构：

    -   必须将**StatusCode**成员设置为 NDIS\_状态\_QOS\_远程\_参数\_更改。

    -   **StatusBuffer**成员必须设置为[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的地址。

    -   **StatusBufferSize**成员必须设置为 `sizeof(NDIS_QOS_PARAMETERS)`。

3.  微型端口驱动程序通过调用[**NdisMIndicateStatusEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)发出状态指示。 驱动程序必须向*StatusIndication*参数传递指向[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构的指针。