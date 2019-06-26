---
title: 确定网络适配器的 VMQ 功能
description: 确定网络适配器的 VMQ 功能
ms.assetid: a8efc393-60fd-4ff8-ba9a-53846f5fbba4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4fa06ce35631fe5e039cc0455027165636764b0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381393"
---
# <a name="determining-the-vmq-capabilities-of-a-network-adapter"></a>确定网络适配器的 VMQ 功能





NDIS 提供接口来确定 VMQ 功能的网络适配器，例如：

-   泛型筛选功能的网络适配器。

-   支持的虚拟机队列功能。

-   预测先行支持允许的网络数据内存将拆分为两个单独缓冲区。

    **请注意**  从 NDIS 6.30 开始，将数据包数据拆分为单独的预测先行缓冲区不再受支持。

     

微型端口驱动程序在网络适配器初始化期间向 NDIS 提供以下信息：

-   网络适配器可以支持 VMQ 硬件功能。

-   当前已启用 VMQ 功能。

-   全局收到启用或禁用网络适配器上的筛选功能。

过量驱动程序和应用程序可以使用以下 OID 查询请求以获取网络适配器的功能。

[OID\_RECEIVE\_FILTER\_HARDWARE\_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)

[OID\_RECEIVE\_FILTER\_CURRENT\_CAPABILITIES](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)

[OID\_接收\_筛选器\_GLOBAL\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters)

NDIS 处理这些 OID 查询请求的微型端口驱动程序。 因此，查询不请求微型端口驱动程序。 NDIS 报告当前已启用在初始化期间接收的网络适配器的 VMQ 功能。 因此，基础驱动程序不需要查询这些 Oid。

[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构指定的网络适配器的筛选功能。 按以下方式使用此结构：

-   当调用 NDIS [ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数，微型端口驱动程序通过初始化来注册其筛选功能[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。 然后，驱动程序设置**HardwareReceiveFilterCapabilities**的成员[ **NDIS\_微型端口\_适配器\_硬件\_ASSIST\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构，以指向**NDIS\_接收\_筛选器\_功能**结构。 驱动程序的下一步调用[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)函数，然后设置*MiniportAttributes*参数指向的**NDIS\_微型端口\_适配器\_硬件\_帮助\_特性**结构。

-   过量的协议驱动程序收到[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构[ **NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)当 NDIS 调用驱动程序的结构[ *ProtocolBindAdapterEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-protocol_bind_adapter_ex)函数。

-   过量的筛选器驱动程序收到[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构[ **NDIS\_筛选器\_附加\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_filter_attach_parameters)当 NDIS 调用驱动程序的结构[ *FilterAttach* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-filter_attach)函数。

-   基础驱动程序收到[ **NDIS\_微型端口\_适配器\_硬件\_协助\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)通过发出的结构OID 查询请求[OID\_接收\_筛选器\_当前\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)或者[OID\_接收\_筛选器\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)。 **HardwareReceiveFilterCapabilities**并**CurrentReceiveFilterCapabilities**成员指向[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构包括以下信息：

<a href="" id="enabledfiltertypes"></a>**EnabledFilterTypes**  
受支持的接收筛选器的类型。 NDIS\_接收\_筛选器\_VMQ\_筛选器\_已启用标志指定是否启用了虚拟机队列 (VMQ) 筛选器。

<a href="" id="enabledqueuetypes"></a>**EnabledQueueTypes**  
支持的类型接收队列。 NDIS\_接收\_筛选器\_VM\_队列\_已启用标志指定是否启用了虚拟机 (VM) 队列。

<a href="" id="numqueues"></a>**NumQueues**  
网络适配器支持接收队列数。 若要支持 VMQ，此数量必须等于或小于 NIC 支持的单播 MAC 地址数。 此数字不能包含默认的队列。

**请注意**  单播 MAC 地址或网络适配器支持的虚拟机队列的数值不包括关联的 NIC 的 MAC 地址

 

<a href="" id="supportedqueueproperties"></a>**SupportedQueueProperties**  
网络适配器支持的队列属性。 NDIS\_接收\_筛选器\_VM\_队列\_支持标志指定的网络适配器提供了支持 VMQ 筛选的最低要求。 支持 VMQ 的 NIC 必须为每个接收队列提供的 MSI X 表条目。 因此，VMQ 微型端口驱动程序必须设置 NDIS\_接收\_筛选器\_MSI\_X\_支持标志。

<a href="" id="supportedfiltertests"></a>**SupportedFilterTests**  
微型端口驱动程序支持的测试操作筛选器。 例如，网络适配器支持测试选定的标头字段，以确定它是否等于给定的值。 VMQ 微型端口驱动程序必须设置 NDIS\_接收\_筛选器\_测试\_标头\_字段\_相等\_支持标志。

<a href="" id="supportedheaders"></a>**SupportedHeaders**  
网络数据包标头的微型端口驱动程序可以检查的类型。 例如，网络适配器可以检查网络数据包的 MAC 标头。 MAC 标头包括数据包类型、 目标和源 MAC 地址、 VLAN 标识符和优先级标记字段。 VMQ 微型端口驱动程序必须设置 NDIS\_接收\_筛选器\_MAC\_标头\_支持标志。

<a href="" id="supportedmacheaderfields"></a>**SupportedMacHeaderFields**  
可以检查微型端口驱动程序的 MAC 标头字段的类型。 VMQ 微型端口驱动程序必须设置 NDIS\_接收\_筛选器\_MAC\_标头\_DEST\_ADDR\_支持标志。

<a href="" id="maxmacheaderfilters"></a>**MaxMacHeaderFilters**  
MAC 标头筛选器的微型端口驱动程序支持的最大数目。 应至少为数量标头的筛选器有 VM 队列。

<a href="" id="maxqueuegroups"></a>**MaxQueueGroups**  
此成员是 ndis 保留。

<a href="" id="maxqueuesperqueuegroup"></a>**MaxQueuesPerQueueGroup**  
此成员是 ndis 保留。

<a href="" id="minlookaheadsplitsize"></a>**MinLookaheadSplitSize**  
最小的大小，以字节为单位，预测先行数据包段为支持的网络适配器。

**请注意**  从 NDIS 6.30 开始，将数据包数据拆分为单独的预测先行缓冲区不再受支持。 支持 NDIS 6.30 或更高版本的微型端口驱动程序必须设置此成员为零。

 

<a href="" id="maxlookaheadsplitsize"></a>**MaxLookaheadSplitSize**  
最大大小，以字节为单位，预测先行数据包段为支持的网络适配器。

**请注意**  从 NDIS 6.30 开始，将数据包数据拆分为单独的预测先行缓冲区不再受支持。 支持 NDIS 6.30 或更高版本的微型端口驱动程序必须设置此成员为零。

 

从成功返回后[OID\_接收\_筛选器\_硬件\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-hardware-capabilities)OID 查询**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向 NDIS\_接收\_筛选器\_功能结构。 这些功能可以包括由 INF 文件设置或通过当前已禁用 VMQ 硬件功能**高级**属性页。 有关详细信息 VMQ INF 文件设置，请参阅[VMQ 标准 INF 条目](https://docs.microsoft.com/windows-hardware/drivers/network/standardized-inf-keywords-for-vmq)。

NDIS 微型端口驱动程序在初始化期间提供的接收筛选硬件功能**HardwareReceiveFilterCapabilities**的成员[ **NDIS\_微型端口\_适配器\_硬件\_协助\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

从成功返回后[OID\_接收\_筛选器\_当前\_功能](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-current-capabilities)OID 查询**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_接收\_筛选器\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。 这些功能包括当前已启用的 VMQ 功能。

当前已启用在初始化期间接收的筛选功能的 NDIS 微型端口驱动程序供应**CurrentReceiveFilterCapabilities**的成员[ **NDIS\_微型端口\_适配器\_硬件\_帮助\_特性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)结构。

NDIS 报告当前已启用接收到过量协议中的驱动程序的筛选功能的基础的网络适配器**ReceiveFilterCapabilities**的成员[ **NDIS\_绑定\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_bind_parameters)绑定操作过程中的结构。

[ **NDIS\_接收\_筛选器\_全局\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)中使用结构[OID\_接收\_筛选器\_GLOBAL\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters)OID 获取当前全局接收筛选器设置的查询。

NDIS\_接收\_筛选器\_GLOBAL\_参数包括以下信息：

<a href="" id="enabledfiltertypes"></a>**EnabledFilterTypes**  
启用类型的接收筛选器。 NDIS\_接收\_筛选器\_VMQ\_筛选器\_已启用标志指定是否启用了虚拟机队列 (VMQ) 筛选器。

<a href="" id="enabledqueuetypes"></a>**EnabledQueueTypes**  
启用类型的接收队列。 NDIS\_接收\_筛选器\_VM\_队列\_已启用标志指定是否启用了虚拟机 (VM) 队列。

从成功返回后[OID\_接收\_筛选器\_全局\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-receive-filter-global-parameters)OID 查询**InformationBuffer**的成员[ **NDIS\_OID\_请求**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_oid_request)结构包含一个指向[ **NDIS\_接收\_筛选器\_GLOBAL\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_receive_filter_global_parameters)结构。 NDIS\_接收\_筛选器\_GLOBAL\_参数结构指定网络适配器上启用或禁用的接收筛选功能。

协议的 NDIS 驱动程序使用 OID\_接收\_筛选器\_GLOBAL\_参数进行查询的当前全局配置参数接收的网络适配器上筛选。 例如，协议驱动程序可以使用此 OID 以确定是否将筛选器类型的接收或接收队列启用或禁用。

 

 





