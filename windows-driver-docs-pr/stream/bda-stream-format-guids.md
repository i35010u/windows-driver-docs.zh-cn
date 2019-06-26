---
title: BDA 流格式 GUID
description: BDA 流格式 GUID
ms.assetid: 216fb02c-b49b-4b9f-b7a5-220c718fb202
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: f5b61b2c961799687e48c993c0ae4f39253c8d9c
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386682"
---
# <a name="bda-stream-format-guids"></a>BDA 流格式 GUID


## <span id="ddk_bda_stream_format_guids_ks"></span><span id="DDK_BDA_STREAM_FORMAT_GUIDS_KS"></span>


BDA 微型驱动程序使用 BDA 流格式的 Guid 来指定它支持的数据格式。 BDA 微型驱动程序将分配这些 Guid 的成员[ **KSDATARANGE** ](https://docs.microsoft.com/previous-versions/ff561658(v=vs.85))结构。 *Bdamedia.h*标头文件定义了这些 Guid。 筛选器的插针指定它们支持连接到的其他筛选器也支持这些范围的 pin 的数据格式的范围。

BDA 中提供了以下流 Guid:

<span id="KSDATAFORMAT_TYPE_BDA_ANTENNA"></span><span id="ksdataformat_type_bda_antenna"></span>KSDATAFORMAT\_TYPE\_BDA\_ANTENNA  
BDA 微型驱动程序分配到此 GUID **MajorFormat**的成员**DataRange**的成员[ **KS\_DATARANGE\_BDA\_天线**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ns-bdamedia-tagks_datarange_bda_antenna)结构以使连接到特定上游筛选器，例如网络提供程序筛选器。

<span id="KSDATAFORMAT_SUBTYPE_BDA_MPEG2_TRANSPORT"></span><span id="ksdataformat_subtype_bda_mpeg2_transport"></span>KSDATAFORMAT\_子类型\_BDA\_MPEG2\_传输  
BDA 微型驱动程序分配到此 GUID**子格式**KSDATARANGE 结构的成员，才能启用连接到的筛选器，还会将分配此 sub 格式的 pin。

<span id="KSDATAFORMAT_SPECIFIER_BDA_TRANSPORT"></span><span id="ksdataformat_specifier_bda_transport"></span>KSDATAFORMAT\_说明符\_BDA\_传输  
BDA 微型驱动程序分配到此 GUID**说明符**KSDATARANGE 结构成员或**DataRange**的成员[ **KS\_DATARANGE\_BDA\_传输**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bdamedia/ns-bdamedia-tagks_datarange_bda_transport)结构以使连接到的筛选器，还会将分配此说明符的 pin。

<span id="KSDATAFORMAT_TYPE_BDA_IF_SIGNAL"></span><span id="ksdataformat_type_bda_if_signal"></span>KSDATAFORMAT\_类型\_BDA\_如果\_信号  
BDA 微型驱动程序分配到此 GUID **MajorFormat** KSDATARANGE 结构的成员，才能启用连接到的筛选器，还会将分配此主要格式的 pin。

<span id="KSDATAFORMAT_TYPE_MPEG2_SECTIONS"></span><span id="ksdataformat_type_mpeg2_sections"></span>KSDATAFORMAT\_TYPE\_MPEG2\_SECTIONS  
BDA 微型驱动程序分配到此 GUID **MajorFormat** KSDATARANGE 结构的成员，才能启用连接到的筛选器，还会将分配此主要格式的 pin。

<span id="KSDATAFORMAT_SUBTYPE_ATSC_SI"></span><span id="ksdataformat_subtype_atsc_si"></span>KSDATAFORMAT\_SUBTYPE\_ATSC\_SI  
BDA 微型驱动程序分配到此 GUID**子格式**KSDATARANGE 结构的成员，才能启用连接到的筛选器，还会将分配此 sub 格式的 pin。

<span id="KSDATAFORMAT_SUBTYPE_DVB_SI"></span><span id="ksdataformat_subtype_dvb_si"></span>KSDATAFORMAT\_SUBTYPE\_DVB\_SI  
BDA 微型驱动程序分配到此 GUID**子格式**KSDATARANGE 结构的成员，才能启用连接到的筛选器，还会将分配此 sub 格式的 pin。

<span id="KSDATAFORMAT_SUBTYPE_BDA_OPENCABLE_PSIP"></span><span id="ksdataformat_subtype_bda_opencable_psip"></span>KSDATAFORMAT\_SUBTYPE\_BDA\_OPENCABLE\_PSIP  
BDA 微型驱动程序分配到此 GUID**子格式**KSDATARANGE 结构的成员，才能启用连接到的筛选器，还会将分配此 sub 格式的 pin。

<span id="KSDATAFORMAT_SUBTYPE_BDA_OPENCABLE_OOB_PSIP"></span><span id="ksdataformat_subtype_bda_opencable_oob_psip"></span>KSDATAFORMAT\_SUBTYPE\_BDA\_OPENCABLE\_OOB\_PSIP  
BDA 微型驱动程序分配到此 GUID**子格式**KSDATARANGE 结构的成员，才能启用连接到的筛选器，还会将分配此 sub 格式的 pin。

<span id="KSDATAFORMAT_TYPE_BDA_IP"></span><span id="ksdataformat_type_bda_ip"></span>KSDATAFORMAT\_TYPE\_BDA\_IP  
BDA 微型驱动程序分配到此 GUID **MajorFormat** KSDATARANGE 结构的成员，才能启用连接到的筛选器，还会将分配此主要格式的 pin。

<span id="KSDATAFORMAT_SUBTYPE_BDA_IP"></span><span id="ksdataformat_subtype_bda_ip"></span>KSDATAFORMAT\_子类型\_BDA\_IP  
BDA 微型驱动程序分配到此 GUID**子格式**KSDATARANGE 结构的成员，才能启用连接到的筛选器，还会将分配此 sub 格式的 pin。

<span id="KSDATAFORMAT_SPECIFIER_BDA_IP"></span><span id="ksdataformat_specifier_bda_ip"></span>KSDATAFORMAT\_SPECIFIER\_BDA\_IP  
BDA 微型驱动程序分配到此 GUID**说明符**KSDATARANGE 结构的成员，才能启用连接到的筛选器，还会将分配此说明符的 pin。

<span id="KSDATAFORMAT_TYPE_BDA_IP_CONTROL"></span><span id="ksdataformat_type_bda_ip_control"></span>KSDATAFORMAT\_类型\_BDA\_IP\_控件  
BDA 微型驱动程序分配到此 GUID **MajorFormat** KSDATARANGE 结构的成员，才能启用连接到的筛选器，还会将分配此主要格式的 pin。

<span id="KSDATAFORMAT_SUBTYPE_BDA_IP_CONTROL"></span><span id="ksdataformat_subtype_bda_ip_control"></span>KSDATAFORMAT\_子类型\_BDA\_IP\_控件  
BDA 微型驱动程序分配到此 GUID**子格式**KSDATARANGE 结构的成员，才能启用连接到的筛选器，还会将分配此 sub 格式的 pin。

<span id="KSDATAFORMAT_TYPE_MPE"></span><span id="ksdataformat_type_mpe"></span>KSDATAFORMAT\_类型\_MPE  
BDA 微型驱动程序分配到此 GUID **MajorFormat** KSDATARANGE 结构的成员，才能启用连接到的筛选器，还会将分配此主要格式的 pin。

 

 





