---
title: 照相机驱动程序结构
description: 以下照相机驱动程序结构是适用于 Windows 10 的新结构。
ms.assetid: E1C2695B-F3E3-4B16-9552-C79B957A5470
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8acbc9a2ef060278a26f6ca32398b4e747113ae1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844756"
---
# <a name="camera-driver-structures"></a>照相机驱动程序结构


以下照相机驱动程序结构是适用于 Windows 10 的新结构。

[**CapturedMetadataExposureCompensation**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagcapturedmetadataexposurecompensation)

[**CapturedMetadataISOGains**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagcapturedmetadataisogains)

[**CapturedMetadataWhiteBalanceGains**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagcapturedmetadatawhitebalancegains)

[**FaceCharacterization**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagfacecharacterization)

[**FaceCharacterizationBlobHeader**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagfacecharacterizationblobheader)

[**FaceRectInfo**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagfacerectinfo)

[**FaceRectInfoBlobHeader**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagfacerectinfoblobheader)

[**HistogramBlobHeader**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-taghistogramblobheader)

[**HistogramDataHeader**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-taghistogramdataheader)

[**HistogramGrid**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-taghistogramgrid)

[**HistogramHeader**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-taghistogramheader)

[**KSCAMERA\_EXTENDEDPROP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_METADATAINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo)

[**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)

[**KSCAMERA\_EXTENDEDPROP\_配置文件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_extendedprop_profile)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcaps)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPSHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcapsheader)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_风险**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_exposure)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_重点**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_focus)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_info)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrol)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROLHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrolheader)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_WHITEBALANCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_whitebalance)

[**KSCAMERA\_ITEMHEADER\_元数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)

[**KSCAMERA\_PHOTOCONFIRMATION\_元数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation)

[**KSCAMERA\_PERFRAMESETTING\_CAP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)

[**KSCAMERA\_PERFRAMESETTING\_CAP\_项\_标题**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_item_header)

[**KSCAMERA\_PERFRAMESETTING\_自定义\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_custom_item)

[**KSCAMERA\_PERFRAMESETTING\_帧\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_frame_header)

[**KSCAMERA\_PERFRAMESETTING\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_header)

[**KSCAMERA\_PERFRAMESETTING\_ITEM\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_item_header)

[**KSCAMERA\_配置文件\_CONCURRENCYINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_concurrencyinfo)

[**KSCAMERA\_配置文件\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_info)

[**KSCAMERA\_配置文件\_MEDIAINFO.XML**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_mediainfo)

[**KSCAMERA\_配置文件\_PININFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_pininfo)

[**KSDEVICE\_配置文件\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksdevice_profile_info)

[**KSDEVICE\_热量\_派单**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_thermal_dispatch)

[**KSPIN\_MDL\_缓存\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_mdl_caching_notification)

[**KSPIN\_MDL\_缓存\_NOTIFICATION32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-kspin_mdl_caching_notification32)

[**KSPROPERTY\_单步执行\_长**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn936838(v=vs.85))

[**KSPROPERTY\_步进\_LONGLONG**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn936841(v=vs.85))

[**KSSTREAM\_元数据\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_metadata_info)

[**KSSTREAM\_UVC\_元数据**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_uvc_metadata)

[**KSSTREAM\_UVC\_METADATATYPE\_时间戳**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_uvc_metadatatype_timestamp)

[**MetadataTimeStamps**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagmetadatatimestamps)

[**MF\_MDL\_共享\_负载\_密钥**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ks/ns-ks-_mf_mdl_shared_payload_key)

 

 




