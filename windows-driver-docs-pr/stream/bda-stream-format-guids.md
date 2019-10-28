---
title: BDA 流格式 GUID
description: BDA 流格式 GUID
ms.assetid: 216fb02c-b49b-4b9f-b7a5-220c718fb202
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ecc7decc5d4f467251b53c2a5981312bb8bd3f83
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840612"
---
# <a name="bda-stream-format-guids"></a>BDA 流格式 GUID


## <span id="ddk_bda_stream_format_guids_ks"></span><span id="DDK_BDA_STREAM_FORMAT_GUIDS_KS"></span>


BDA 微型驱动程序使用 BDA 流格式 Guid 来指定它所支持的数据格式。 BDA 微型驱动程序将这些 Guid 分配给[**KSDATARANGE**](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构的成员。 *Bdamedia*头文件定义这些 guid。 筛选器的 pin 指定它们支持的数据格式范围，以连接到还支持这些范围的其他筛选器的 pin。

BDA 中提供了以下流 Guid：

<span id="KSDATAFORMAT_TYPE_BDA_ANTENNA"></span><span id="ksdataformat_type_bda_antenna"></span>KSDATAFORMAT\_类型\_BDA\_天线  
BDA 微型驱动程序将此 GUID 分配给[**KS\_DataRange\_BDA\_天线**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ns-bdamedia-tagks_datarange_bda_antenna)结构的**DataRange**成员的**MajorFormat**成员，以启用连接到特定上游筛选器，例如网络提供程序筛选器.

<span id="KSDATAFORMAT_SUBTYPE_BDA_MPEG2_TRANSPORT"></span><span id="ksdataformat_subtype_bda_mpeg2_transport"></span>KSDATAFORMAT\_子类型\_BDA\_MPEG2\_传输  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**SubFormat**成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_SPECIFIER_BDA_TRANSPORT"></span><span id="ksdataformat_specifier_bda_transport"></span>KSDATAFORMAT\_BDA\_传输\_说明符  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**说明符**成员或[**KS\_DataRange\_BDA\_传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/bdamedia/ns-bdamedia-tagks_datarange_bda_transport)结构的**DataRange**成员，以启用连接到还分配此说明符。

<span id="KSDATAFORMAT_TYPE_BDA_IF_SIGNAL"></span><span id="ksdataformat_type_bda_if_signal"></span>如果\_信号，则 KSDATAFORMAT\_键入\_BDA\_  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**MajorFormat**成员，以允许连接到也分配此主要格式的筛选器的 pin。

<span id="KSDATAFORMAT_TYPE_MPEG2_SECTIONS"></span><span id="ksdataformat_type_mpeg2_sections"></span>KSDATAFORMAT\_键入\_MPEG2\_部分  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**MajorFormat**成员，以允许连接到也分配此主要格式的筛选器的 pin。

<span id="KSDATAFORMAT_SUBTYPE_ATSC_SI"></span><span id="ksdataformat_subtype_atsc_si"></span>KSDATAFORMAT\_子类型\_ATSC\_SI  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**SubFormat**成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_SUBTYPE_DVB_SI"></span><span id="ksdataformat_subtype_dvb_si"></span>KSDATAFORMAT\_子类型\_DVB\_SI  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**SubFormat**成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_SUBTYPE_BDA_OPENCABLE_PSIP"></span><span id="ksdataformat_subtype_bda_opencable_psip"></span>KSDATAFORMAT\_子类型\_BDA\_OPENCABLE\_PSIP  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**SubFormat**成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_SUBTYPE_BDA_OPENCABLE_OOB_PSIP"></span><span id="ksdataformat_subtype_bda_opencable_oob_psip"></span>KSDATAFORMAT\_子类型\_BDA\_OPENCABLE\_OOB\_PSIP  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**SubFormat**成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_TYPE_BDA_IP"></span><span id="ksdataformat_type_bda_ip"></span>KSDATAFORMAT\_类型\_BDA\_IP  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**MajorFormat**成员，以允许连接到也分配此主要格式的筛选器的 pin。

<span id="KSDATAFORMAT_SUBTYPE_BDA_IP"></span><span id="ksdataformat_subtype_bda_ip"></span>KSDATAFORMAT\_子类型\_BDA\_IP  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**SubFormat**成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_SPECIFIER_BDA_IP"></span><span id="ksdataformat_specifier_bda_ip"></span>KSDATAFORMAT\_说明符\_BDA\_IP  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**说明符**成员，以允许连接到还分配此说明符的筛选器的 pin。

<span id="KSDATAFORMAT_TYPE_BDA_IP_CONTROL"></span><span id="ksdataformat_type_bda_ip_control"></span>KSDATAFORMAT\_键入\_BDA\_IP\_控制  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**MajorFormat**成员，以允许连接到也分配此主要格式的筛选器的 pin。

<span id="KSDATAFORMAT_SUBTYPE_BDA_IP_CONTROL"></span><span id="ksdataformat_subtype_bda_ip_control"></span>KSDATAFORMAT\_子类型\_BDA\_IP\_控制  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**SubFormat**成员，以允许连接到还分配此子格式的筛选器的 pin。

<span id="KSDATAFORMAT_TYPE_MPE"></span><span id="ksdataformat_type_mpe"></span>KSDATAFORMAT\_类型\_MPE  
BDA 微型驱动程序将此 GUID 分配给 KSDATARANGE 结构的**MajorFormat**成员，以允许连接到也分配此主要格式的筛选器的 pin。

 

 





