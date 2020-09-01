---
title: BDA 筛选器类别 GUID
description: BDA 筛选器类别 GUID
ms.assetid: fbd4bf91-8309-423a-97ea-7e4f90cd3b68
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d5d2ec0a931a1133c6dfcc52dc588de923d76f2
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185411"
---
# <a name="bda-filter-category-guids"></a>BDA 筛选器类别 GUID


## <span id="ddk_bda_filter_category_guids_ks"></span><span id="DDK_BDA_FILTER_CATEGORY_GUIDS_KS"></span>


BDA 微型驱动程序使用 BDA 筛选器类别 Guid 来指定要创建的 BDA 筛选器的类型。 BDA 微型驱动程序将这些 Guid 分配给[**KSFILTER \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksfilter_descriptor)结构的**类别**成员指向的数组。 *Bdamedia*头文件定义这些 guid。

BDA 中提供以下筛选器类别 Guid：

<span id="KSCATEGORY_BDA_RECEIVER_COMPONENT"></span><span id="kscategory_bda_receiver_component"></span>KSCATEGORY \_ BDA \_ 接收器 \_ 组件  
BDA 微型驱动程序将此 GUID 分配给指定以创建 BDA 接收方筛选器。

<span id="KSCATEGORY_BDA_NETWORK_TUNER"></span><span id="kscategory_bda_network_tuner"></span>KSCATEGORY \_ BDA \_ 网络 \_ 调谐器  
BDA 微型驱动程序将此 GUID 分配给指定以创建 BDA 网络调谐器筛选器。

<span id="KSCATEGORY_BDA_NETWORK_EPG"></span><span id="kscategory_bda_network_epg"></span>KSCATEGORY \_ BDA \_ 网络 \_ EPG  
BDA 微型驱动程序分配此 GUID 以指定创建 (EPG) 筛选器的 BDA 电子收视指南。

<span id="KSCATEGORY_BDA_IP_SINK"></span><span id="kscategory_bda_ip_sink"></span>KSCATEGORY \_ BDA \_ IP \_ 接收器  
BDA 微型驱动程序分配此 GUID 以指定创建一个 BDA IP 接收器筛选器。

<span id="KSCATEGORY_BDA_NETWORK_PROVIDER"></span><span id="kscategory_bda_network_provider"></span>KSCATEGORY \_ BDA \_ 网络 \_ 提供程序  
BDA 微型驱动程序将此 GUID 分配给指定以创建 BDA 网络提供程序筛选器。

<span id="KSCATEGORY_BDA_TRANSPORT_INFORMATION"></span><span id="kscategory_bda_transport_information"></span>KSCATEGORY \_ BDA \_ 传输 \_ 信息  
BDA 微型驱动程序将此 GUID 分配给指定，以创建 (.TIF) 的 BDA 传输信息筛选器。

 

