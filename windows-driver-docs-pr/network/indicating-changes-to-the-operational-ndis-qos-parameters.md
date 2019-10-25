---
title: 指示对 NDIS QoS 操作参数的更改
description: 指示对 NDIS QoS 操作参数的更改
ms.assetid: BAE99C83-2732-4216-BC49-23F541AA3F10
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 575876f14ba851747a6037e2215c65365cadb905
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824715"
---
# <a name="indicating-changes-to-the-operational-ndis-qos-parameters"></a>指示对 NDIS QoS 操作参数的更改


支持 NDIS 服务质量（QoS）的微型端口驱动程序发出[**ndis\_状态\_QoS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示（当驱动程序的操作 NDIS QoS 参数为首次或在稍后更改时解决。 微型端口驱动程序用这些操作参数配置网络适配器，以执行 QoS 数据包传输。

微型端口驱动程序必须遵循以下指导原则，使[**NDIS\_状态\_QOS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示：

-   微型端口驱动程序必须在[ **\_QOS\_操作\_参数时发出 NDIS\_状态，\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示，然后再解决它的操作 NDIS QOS 参数并配置网络适配器.

    **注意** 如果使用注册表中的专有本地 NDIS QoS 参数设置微型端口驱动程序，则驱动程序必须[ **\_QoS\_操作\_参数发出 NDIS\_状态，\_** ](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)在或期间更改状态指示紧跟在对[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)的调用之后。 在这种情况下，驱动程序使用其专用的本地 NDIS QoS 参数设置初始化[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构。

    有关驱动程序如何解析其操作 NDIS QoS 参数设置的详细信息，请参阅[解决操作 Ndis qos](resolving-operational-ndis-qos-parameters.md)参数。

-   在此初始状态指示后，微型端口驱动程序应[ **\_QOS\_运行\_参数**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)，在其操作 ndis QOS 参数发生更改时，将 NDIS\_状态颁发给\_更改状态指示。 例如，在下列情况下，操作 NDIS QoS 参数可能会更改：

    -   由于更改了本地 NDIS QoS 参数，操作 NDIS QoS 参数会发生更改。 这些参数可以通过 oid [\_QOS 方法请求\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-qos-parameters)或通过独立硬件供应商（IHV）开发的管理应用程序来更改。

    -   由于与远程对等节点的 QoS 设置发生冲突，操作 NDIS QoS 参数发生更改。

        微型端口驱动程序使用 IEEE 802.1 Qaz 数据中心桥接交换（DCBX）协议来发现远程对等机的 QoS 参数。 如果启用 "DCBX" 状态，则驱动程序必须按照为 DCBX 状态引擎定义的过程来解决其 QoS 参数与远程对等的 QoS 参数之间的差异。 有关此状态引擎的详细信息，请参阅 IEEE 802.1 Qaz 草案标准。

        有关本地 DCBX 适用状态的详细信息，请参阅[管理本地 DCBX 适用的状态](managing-the-local-dcbx-willing-state.md)。

    **注意** 当微型端口驱动程序收到本地或远程 NDIS QoS 参数时，它不应发出[**NDIS\_状态\_QoS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示（如果没有任何更改）操作 NDIS QoS 参数。 如果驱动程序导致这种不必要的状态指示，NDIS 可能不会将指示传递到过量驱动程序。

-   当需要替代用于解析操作 NDIS 的本地 NDIS QoS 参数时，微型端口驱动程序应[ **\_QOS\_操作\_参数发出 NDIS\_状态，\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示QoS 参数。

    微型端口驱动程序通过发出[**ndis\_状态\_QoS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示，通知 NDIS 和过量驱动程序已覆盖了本地 NDIS QoS 参数。 对于这种类型的指示，驱动程序必须将相应的**ndis\_qos\_参数\_*Xxx*\_** 在[**NDIS\_Qos\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的**flags**成员中更改的标志指定替代本地 NDIS QoS 参数的原因。

    有关微型端口驱动程序如何管理本地 QoS 参数的详细信息，请参阅[设置本地 NDIS Qos 参数](setting-local-ndis-qos-parameters.md)。

    有关微型端口驱动程序如何解析其操作 QoS 参数的详细信息，请参阅[解决操作 NDIS Qos 参数](resolving-operational-ndis-qos-parameters.md)。

**注意** 如果当前通过 **\_qos**关键字启用了其 ndis QOS 功能，微型端口驱动程序必须发出[**ndis\_状态\_QOS\_操作\_参数\*更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示标准化 INF 关键字。 有关详细信息，请参阅[NDIS QoS 的标准化 INF 关键字](standardized-inf-keywords-for-ndis-qos.md)。

## <a name="guidelines-for-issuing-the-ndis_status_qos_operational_parameters_change-status-indication"></a>有关将 NDIS\_状态\_QOS\_操作\_参数\_更改状态指示的准则


小型端口驱动程序在发出 NDIS\_状态时遵循这些步骤[ **\_QOS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示：

1.  微型端口驱动程序分配一个足够大的缓冲区，以包含以下内容：

    -   [**Ndis\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构，其中包含 ndis qos 配置设置，以及 ndis qos 通信类的全局操作参数。

    -   一组[**NDIS\_QOS\_分类\_元素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)结构。 其中每个结构都指定了由数据包数据模式（*条件*）和关联的 IEEE 802.1 p 优先级（*操作*）定义的流量分类。 如果网络适配器在传输或*传出*数据包中找到与条件匹配的模式，则它会将关联的优先级分配给数据包。 该适配器还会将其他 NDIS QoS 策略应用到基于优先级别的数据包。

2.  小型端口将[**ndis\_qos\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构与操作 ndis QOS 参数一起初始化。 驱动程序必须提供一组完整的操作参数，其中包括那些可能未在网络适配器上配置的参数。

    当微型端口驱动程序初始化**标头**成员时，它会将**标头**的**类型**成员设置为 NDIS\_对象\_类型\_QOS\_参数。 微型端口驱动程序将**标头**的**修订**成员设置为 NDIS\_QOS\_参数\_修订版本\_1，将**Size**成员设置为 ndis\_\_qos\_\_\_1。

    小型端口驱动程序将相应的**NDIS\_QOS\_参数\_*Xxx*\_** 在**flags**成员中更改的标志。[**NDIS\_状态\_QOS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示。

    **注意**  将**NDIS\_QOS\_参数设置\_*XXX*\_更改**的标志是可选的。 NDIS 始终假定[**ndis\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)的成员是最新的，即使它们未更改为以前的[**NDIS\_状态\_QOS\_操作\_参数\_更改**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-qos-operational-parameters-change)状态指示。

    有关如何设置**标志**成员的详细信息，请参阅[设置**标志**成员的准则](#guidelines-for-setting-the-flags-member)。

3.  微型端口驱动程序通过操作 NDIS QoS 参数中的每个通信分类初始化[**NDIS\_QOS\_分类\_元素**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)结构。 驱动程序在[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的末尾添加这些元素。

    **注意** 微型端口驱动程序不得将 NDIS\_QOS\_分类\_强制实施\_，\_[**qos\_分类**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element)\_的元素结构的**标志**成员中\_微型端口标志。

    驱动程序将[**NDIS\_QOS\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构的**NumClassificationElements**成员设置为数组中分类元素的数目。 驱动程序将**FirstClassificationElementOffset**成员设置为缓冲区开头的第一个元素的字节偏移量。 驱动程序还将**ClassificationElementSize**成员设置为数组中每个元素的长度（以字节为单位）。

    **注意** 从 NDIS 6.30 开始，微型端口驱动程序必须将**ClassificationElementSize**成员设置为 `sizeof(NDIS_QOS_CLASSIFICATION_ELEMENT`）。

4.  微型端口驱动程序通过以下方式初始化状态指示的[**NDIS\_状态\_指示**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)结构：

    -   必须将**StatusCode**成员设置为 NDIS\_状态\_QOS\_操作\_参数\_更改。

    -   **StatusBuffer**成员必须设置为指向包含操作 NDIS QoS 参数的缓冲区的指针。

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

**注意** 如果[**ndis\_qos\_parameters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters)结构包含 ndis QOS 参数设置，则必须设置 **\_qos\_参数\_*Xxx*\_配置**的标志。 无论设置是否已更改，微型端口驱动程序都必须设置这些标志。 但是，驱动程序必须将**NDIS\_QOS\_\_\_参数** 设置为仅对那些已更改的设置设置为 "已更改" 的标记。