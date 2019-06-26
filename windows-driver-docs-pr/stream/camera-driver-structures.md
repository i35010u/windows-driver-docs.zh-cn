---
title: 照相机的驱动程序结构
description: 以下的照相机的驱动程序结构是适用于 Windows 10 新功能。
ms.assetid: E1C2695B-F3E3-4B16-9552-C79B957A5470
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69ebb67e27d1a18476374c1b60d29aea0d36b09e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386667"
---
# <a name="camera-driver-structures"></a>照相机的驱动程序结构


以下的照相机的驱动程序结构是适用于 Windows 10 新功能。

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

[**KSCAMERA\_EXTENDEDPROP\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA\_EXTENDEDPROP\_METADATAINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo)

[**KSCAMERA\_EXTENDEDPROP\_PHOTOMODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)

[**KSCAMERA\_EXTENDEDPROP\_PROFILE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_kscamera_extendedprop_profile)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcaps)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_CONFIGCAPSHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcapsheader)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_EXPOSURE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_exposure)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_FOCUS**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_focus)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_info)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrol)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_ISPCONTROLHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrolheader)

[**KSCAMERA\_EXTENDEDPROP\_ROI\_WHITEBALANCE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_whitebalance)

[**KSCAMERA\_元数据\_ITEMHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)

[**KSCAMERA\_元数据\_PHOTOCONFIRMATION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation)

[**KSCAMERA\_PERFRAMESETTING\_CAP\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)

[**KSCAMERA\_PERFRAMESETTING\_CAP\_项\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_item_header)

[**KSCAMERA\_PERFRAMESETTING\_自定义\_项**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_custom_item)

[**KSCAMERA\_PERFRAMESETTING\_FRAME\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_frame_header)

[**KSCAMERA\_PERFRAMESETTING\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_header)

[**KSCAMERA\_PERFRAMESETTING\_ITEM\_HEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-kscamera_perframesetting_item_header)

[**KSCAMERA\_配置文件\_CONCURRENCYINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_kscamera_profile_concurrencyinfo)

[**KSCAMERA\_配置文件\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_kscamera_profile_info)

[**KSCAMERA\_配置文件\_MEDIAINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_kscamera_profile_mediainfo)

[**KSCAMERA\_配置文件\_PININFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_kscamera_profile_pininfo)

[**KSDEVICE\_PROFILE\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ksmedia/ns-ksmedia-_ksdevice_profile_info)

[**KSDEVICE\_THERMAL\_DISPATCH**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_ksdevice_thermal_dispatch)

[**KSPIN\_MDL\_CACHING\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_mdl_caching_notification)

[**KSPIN\_MDL\_CACHING\_NOTIFICATION32**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-kspin_mdl_caching_notification32)

[**KSPROPERTY\_单步执行\_长**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn936838(v=vs.85))

[**KSPROPERTY\_单步执行\_LONGLONG**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/dn936841(v=vs.85))

[**KSSTREAM\_元数据\_信息**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_metadata_info)

[**KSSTREAM\_UVC\_METADATA**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_uvc_metadata)

[**KSSTREAM\_UVC\_METADATATYPE\_TIMESTAMP**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-ksstream_uvc_metadatatype_timestamp)

[**MetadataTimeStamps**](https://docs.microsoft.com/windows/desktop/api/mfapi/ns-mfapi-tagmetadatatimestamps)

[**MF\_MDL\_共享\_负载\_密钥**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ks/ns-ks-_mf_mdl_shared_payload_key)

 

 




