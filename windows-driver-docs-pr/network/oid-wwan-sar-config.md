---
title: OID_WWAN_SAR_CONFIG
description: OID_WWAN_SAR_CONFIG 获取或设置有关移动宽带 (MB) 设备的特定吸收速率 （特别行政区） 中，退避模式和级别的信息。
ms.assetid: 78B049E0-A80E-42AA-9D81-D45BBCF84FCB
ms.date: 08/17/2018
keywords: -从 Windows Vista 开始 OID_WWAN_SAR_CONFIG 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: bbeb8edcb8140c506cdcedb96d867c0488a35a43
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63368255"
---
# <a name="oidwwansarconfig"></a>OID_WWAN_SAR_CONFIG

OID_WWAN_SAR_CONFIG 获取或设置有关移动宽带 (MB) 设备的特定吸收速率 （特别行政区） 中，退避模式和级别的信息。 

微型端口驱动程序必须处理查询请求，一开始以异步方式返回 NDIS_STATUS_INDICATION_REQUIRED 到原始请求更高版本发送前[NDIS_STATUS_WWAN_SAR_CONFIG](ndis-status-wwan-sar-config.md)状态通知包含[ **NDIS_WWAN_SAR_CONFIG_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)结构，描述当前特别行政区配置。

对于组的请求，此 OID 负载包含[ **NDIS_WWAN_SET_SAR_CONFIG** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_config)结构，它指定新特别行政区配置调制解调器。

## <a name="remarks"></a>备注

每个查询或一组请求后，微型端口驱动程序应返回[ **NDIS_WWAN_SAR_CONFIG_INFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)结构，其中包含与移动宽带关联的设备上所有天线的信息.

有关此 OID 的使用情况的详细信息，请参阅[MBIM_CID_MS_SAR_CONFIG](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support#mbimcidmssarconfig)。

## <a name="requirements"></a>要求

|   |   |
| --- | --- |
| Version | Windows 10 版本 1703 |
| Header | Ntddndis.h （包括 Ndis.h） |

## <a name="see-also"></a>请参阅

[MB 特别行政区平台支持](https://docs.microsoft.com/windows-hardware/drivers/network/mb-sar-platform-support)

[NDIS_STATUS_WWAN_SAR_CONFIG](ndis-status-wwan-sar-config.md)

[**NDIS_WWAN_SAR_CONFIG_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_sar_config_info)

[**NDIS_WWAN_SET_SAR_CONFIG**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_set_sar_config)
