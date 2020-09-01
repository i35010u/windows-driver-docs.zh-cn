---
title: 照相机驱动程序结构
description: 以下照相机驱动程序结构是适用于 Windows 10 的新结构。
ms.assetid: E1C2695B-F3E3-4B16-9552-C79B957A5470
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab16c20817f45e7a4f5a3dd0e2605f0ab3f8855a
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191443"
---
# <a name="camera-driver-structures"></a>照相机驱动程序结构


以下照相机驱动程序结构是适用于 Windows 10 的新结构。

[**CapturedMetadataExposureCompensation**](/windows/win32/api/mfapi/ns-mfapi-tagcapturedmetadataexposurecompensation)

[**CapturedMetadataISOGains**](/windows/win32/api/mfapi/ns-mfapi-tagcapturedmetadataisogains)

[**CapturedMetadataWhiteBalanceGains**](/windows/win32/api/mfapi/ns-mfapi-tagcapturedmetadatawhitebalancegains)

[**FaceCharacterization**](/windows/win32/api/mfapi/ns-mfapi-tagfacecharacterization)

[**FaceCharacterizationBlobHeader**](/windows/win32/api/mfapi/ns-mfapi-tagfacecharacterizationblobheader)

[**FaceRectInfo**](/windows/win32/api/mfapi/ns-mfapi-tagfacerectinfo)

[**FaceRectInfoBlobHeader**](/windows/win32/api/mfapi/ns-mfapi-tagfacerectinfoblobheader)

[**HistogramBlobHeader**](/windows/win32/api/mfapi/ns-mfapi-taghistogramblobheader)

[**HistogramDataHeader**](/windows/win32/api/mfapi/ns-mfapi-taghistogramdataheader)

[**HistogramGrid**](/windows/win32/api/mfapi/ns-mfapi-taghistogramgrid)

[**HistogramHeader**](/windows/win32/api/mfapi/ns-mfapi-taghistogramheader)

[**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)

[**KSCAMERA \_ EXTENDEDPROP \_ METADATAINFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo)

[**KSCAMERA \_ EXTENDEDPROP \_ PHOTOMODE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode)

[**KSCAMERA \_ EXTENDEDPROP \_ 配置文件**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_extendedprop_profile)

[**KSCAMERA \_ EXTENDEDPROP \_ 投资回报 \_ CONFIGCAPS**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcaps)

[**KSCAMERA \_ EXTENDEDPROP \_ 投资回报 \_ CONFIGCAPSHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcapsheader)

[**KSCAMERA \_ EXTENDEDPROP \_ 投资回报率 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_exposure)

[**KSCAMERA \_ EXTENDEDPROP \_ 投资回报 \_ 要点**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_focus)

[**KSCAMERA \_ EXTENDEDPROP \_ 投资回报 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_info)

[**KSCAMERA \_ EXTENDEDPROP \_ 投资回报 \_ ISPCONTROL**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrol)

[**KSCAMERA \_ EXTENDEDPROP \_ 投资回报 \_ ISPCONTROLHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrolheader)

[**KSCAMERA \_ EXTENDEDPROP \_ 投资回报 \_ WHITEBALANCE**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_whitebalance)

[**KSCAMERA \_ 元数据 \_ ITEMHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader)

[**KSCAMERA \_ 元数据 \_ PHOTOCONFIRMATION**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation)

[**KSCAMERA \_ PERFRAMESETTING \_ CAP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header)

[**KSCAMERA \_ PERFRAMESETTING \_ CAP \_ 项 \_ 标题**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_item_header)

[**KSCAMERA \_ PERFRAMESETTING \_ 自定义 \_ 项**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_custom_item)

[**KSCAMERA \_ PERFRAMESETTING \_ 框架 \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_frame_header)

[**KSCAMERA \_ PERFRAMESETTING \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_header)

[**KSCAMERA \_ PERFRAMESETTING \_ 项 \_ 标题**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_item_header)

[**KSCAMERA \_ 配置文件 \_ CONCURRENCYINFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_concurrencyinfo)

[**KSCAMERA \_ 配置文件 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_info)

[**KSCAMERA \_ 配置文件 \_ MEDIAINFO.XML**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_mediainfo)

[**KSCAMERA \_ 配置文件 \_ PININFO**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_pininfo)

[**KSDEVICE \_ 配置文件 \_ 信息**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksdevice_profile_info)

[**KSDEVICE \_ 散热 \_ 派单**](/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_thermal_dispatch)

[**KSPIN \_ MDL \_ 缓存 \_ 通知**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_mdl_caching_notification)

[**KSPIN \_ MDL \_ 缓存 \_ NOTIFICATION32**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_mdl_caching_notification32)

[**KSPROPERTY \_ 步进 \_ 长**](/previous-versions/windows/hardware/drivers/dn936838(v=vs.85))

[**KSPROPERTY \_ 步进 \_ LONGLONG**](/previous-versions/windows/hardware/drivers/dn936841(v=vs.85))

[**KSSTREAM \_ 元数据 \_ 信息**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_metadata_info)

[**KSSTREAM \_ UVC \_ 元数据**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_uvc_metadata)

[**KSSTREAM \_ UVC \_ METADATATYPE \_ 时间戳**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_uvc_metadatatype_timestamp)

[**MetadataTimeStamps**](/windows/win32/api/mfapi/ns-mfapi-tagmetadatatimestamps)

[**MF \_ MDL \_ 共享 \_ 负载 \_ 密钥**](/windows-hardware/drivers/ddi/ks/ns-ks-_mf_mdl_shared_payload_key)

 

