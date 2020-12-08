---
title: BDA 流格式 GUID
description: BDA 流格式 GUID
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 082d9293b2b8a748368d61a559c576706a728de4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802173"
---
# <a name="bda-stream-format-guids"></a>BDA 流格式 GUID


## <span id="ddk_bda_stream_format_guids_ks"></span><span id="DDK_BDA_STREAM_FORMAT_GUIDS_KS"></span>


BDA 微型驱动程序使用 BDA 流格式 Guid 来指定它所支持的数据格式。 BDA 微型驱动程序将这些 Guid 分配给 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85)) 结构的成员。 *Bdamedia* 头文件定义这些 guid。 筛选器的 pin 指定它们支持的数据格式范围，以连接到还支持这些范围的其他筛选器的 pin。

BDA 中提供了以下流 Guid：

<span id="KSDATAFORMAT_TYPE_BDA_ANTENNA"></span><span id="ksdataformat_type_bda_antenna"></span>KSDATAFORMAT \_ 类型 \_ BDA \_ 天线  
BDA 微型驱动程序将此 GUID 分配给 [**KS \_ DataRange \_ BDA \_ 天线**](/windows-hardware/drivers/ddi/bdamedia/ns-bdamedia-tagks_datarange_bda_antenna)结构的 **DataRange** 成员的 **MajorFormat** 成员，以启用连接到特定上游筛选器，例如网络提供程序筛选器。

<span id="KSDATAFORMAT_SUBTYPE_BDA_MPEG2_TRANSPORT"></span><span id="ksdataformat_subtype_bda_mpeg2_transport"></span>KSDATAFORMAT \_ 子类型 \_ BDA \_ MPEG2 \_ 传输  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **SubFormat** 成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_SPECIFIER_BDA_TRANSPORT"></span><span id="ksdataformat_specifier_bda_transport"></span>KSDATAFORMAT \_ 说明符 \_ BDA \_ 传输  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **说明符** 成员或 [**KS \_ DataRange \_ BDA \_ 传输**](/windows-hardware/drivers/ddi/bdamedia/ns-bdamedia-tagks_datarange_bda_transport)结构的 **DataRange** 成员，以启用连接到也分配此说明符的筛选器的 pin。

<span id="KSDATAFORMAT_TYPE_BDA_IF_SIGNAL"></span><span id="ksdataformat_type_bda_if_signal"></span>KSDATAFORMAT \_ \_ \_ 如果信号，则键入 BDA \_  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **MajorFormat** 成员，以允许连接到也分配此主要格式的筛选器的 pin。

<span id="KSDATAFORMAT_TYPE_MPEG2_SECTIONS"></span><span id="ksdataformat_type_mpeg2_sections"></span>KSDATAFORMAT \_ 类型 \_ MPEG2 \_ 部分  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **MajorFormat** 成员，以允许连接到也分配此主要格式的筛选器的 pin。

<span id="KSDATAFORMAT_SUBTYPE_ATSC_SI"></span><span id="ksdataformat_subtype_atsc_si"></span>KSDATAFORMAT \_ 子类型 \_ ATSC \_ SI  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **SubFormat** 成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_SUBTYPE_DVB_SI"></span><span id="ksdataformat_subtype_dvb_si"></span>KSDATAFORMAT \_ 子类型 \_ DVB \_ SI  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **SubFormat** 成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_SUBTYPE_BDA_OPENCABLE_PSIP"></span><span id="ksdataformat_subtype_bda_opencable_psip"></span>KSDATAFORMAT \_ 子类型 \_ BDA \_ OPENCABLE \_ PSIP  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **SubFormat** 成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_SUBTYPE_BDA_OPENCABLE_OOB_PSIP"></span><span id="ksdataformat_subtype_bda_opencable_oob_psip"></span>KSDATAFORMAT \_ 子类型 \_ BDA \_ OPENCABLE \_ OOB \_ PSIP  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **SubFormat** 成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_TYPE_BDA_IP"></span><span id="ksdataformat_type_bda_ip"></span>KSDATAFORMAT \_ 类型的 \_ BDA \_ IP  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **MajorFormat** 成员，以允许连接到也分配此主要格式的筛选器的 pin。

<span id="KSDATAFORMAT_SUBTYPE_BDA_IP"></span><span id="ksdataformat_subtype_bda_ip"></span>KSDATAFORMAT \_ 子类型 \_ BDA \_ IP  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **SubFormat** 成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_SPECIFIER_BDA_IP"></span><span id="ksdataformat_specifier_bda_ip"></span>KSDATAFORMAT \_ 说明符 \_ BDA \_ IP  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **说明符** 成员，以允许连接到还分配此说明符的筛选器的 pin。

<span id="KSDATAFORMAT_TYPE_BDA_IP_CONTROL"></span><span id="ksdataformat_type_bda_ip_control"></span>KSDATAFORMAT \_ 类型 \_ BDA \_ IP \_ 控制  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **MajorFormat** 成员，以允许连接到也分配此主要格式的筛选器的 pin。

<span id="KSDATAFORMAT_SUBTYPE_BDA_IP_CONTROL"></span><span id="ksdataformat_subtype_bda_ip_control"></span>KSDATAFORMAT \_ 子类型 \_ BDA \_ IP \_ 控制  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **SubFormat** 成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_TYPE_MPE"></span><span id="ksdataformat_type_mpe"></span>KSDATAFORMAT \_ 类型 \_ MPE  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的 **MajorFormat** 成员，以允许连接到也分配此主要格式的筛选器的 pin。

 

