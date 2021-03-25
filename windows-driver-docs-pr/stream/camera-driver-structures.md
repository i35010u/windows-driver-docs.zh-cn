---
title: 适用于 Windows 10 的通用照相机驱动程序结构
description: 提供有关适用于 Windows 10 的通用照相机驱动程序结构的信息。
ms.date: 03/23/2021
ms.localizationpriority: medium
ms.openlocfilehash: 7df8024363447b0c9852d11282816f94b7d687ae
ms.sourcegitcommit: 2a27786ed72024f064bbfef20933b0d0b429d4b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/25/2021
ms.locfileid: "105106155"
---
# <a name="universal-camera-driver-structures-for-windows-10"></a>适用于 Windows 10 的通用照相机驱动程序结构

适用于 Windows 10 的相机驱动程序接口已聚合到所有设备，并使用通用照相机驱动程序模型。

以下主题提供有关适用于 Windows 10 的通用照相机驱动程序结构的信息：

| 标题 | 说明 |
|--|--|
| [CapturedMetadataExposureCompensation](/windows/win32/api/mfapi/ns-mfapi-capturedmetadataexposurecompensation) | 此结构包含已捕获照片的 EV 补偿反馈的 blob 信息。 |
| [CapturedMetadataISOGains](/windows/win32/api/mfapi/ns-mfapi-capturedmetadataisogains) | CapturedMetadataISOGains 结构描述 MF_CAPTURE_METADATA_ISO_GAINS 的 blob 格式。 |
| [CapturedMetadataWhiteBalanceGains](/windows/win32/api/mfapi/ns-mfapi-capturedmetadatawhitebalancegains) | 此结构描述 MF_CAPTURE_METADATA_WHITEBALANCE_GAINS 特性的 blob 格式。 |
| [FaceCharacterization](/windows/win32/api/mfapi/ns-mfapi-facecharacterization) | FaceCharacterization 结构描述 MF_CAPTURE_METADATA_FACEROICHARACTERIZATIONS 特性的 blob 格式。 |
| [FaceCharacterizationBlobHeader](/windows/win32/api/mfapi/ns-mfapi-facecharacterizationblobheader) | FaceCharacterizationBlobHeader 结构描述 MF_CAPTURE_METADATA_FACEROICHARACTERIZATIONS 属性的 blob 格式的大小和计数信息。 |
| [FaceRectInfo](/windows/win32/api/mfapi/ns-mfapi-facerectinfo) | FaceRectInfo 结构描述 MF_CAPTURE_METADATA_FACEROIS 特性的 blob 格式。 |
| [FaceRectInfoBlobHeader](/windows/win32/api/mfapi/ns-mfapi-facerectinfoblobheader) | FaceRectInfoBlobHeader 结构描述 MF_CAPTURE_METADATA_FACEROIS 属性的 blob 格式的大小和计数信息。 |
| [HistogramBlobHeader](/windows/win32/api/mfapi/ns-mfapi-histogramblobheader) | HistogramBlobHeader 结构描述 MF_CAPTURE_METADATA_HISTOGRAM 属性的 blob 中的 blob 大小和直方图数。 |
| [HistogramDataHeader](/windows/win32/api/mfapi/ns-mfapi-histogramdataheader) | HistogramDataHeader 结构描述 MF_CAPTURE_METADATA_HISTOGRAM 特性的 blob 格式。 |
| [HistogramGrid](/windows/win32/api/mfapi/ns-mfapi-histogramgrid) | HistogramGrid 结构描述 MF_CAPTURE_METADATA_HISTOGRAM 的 blob 格式。 |
| [HistogramHeader](/windows/win32/api/mfapi/ns-mfapi-histogramheader) | HistogramHeader 结构描述 MF_CAPTURE_METADATA_HISTOGRAM 的 blob 格式。 |
| [KSCAMERA_EXTENDEDPROP_HEADER](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) | KSCAMERA_EXTENDEDPROP_HEADER 结构是扩展控件属性的负载标头。 |
| [KSCAMERA_EXTENDEDPROP_METADATAINFO](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_metadatainfo) | 此结构表示扩展属性控件的元数据信息。 |
| [KSCAMERA_EXTENDEDPROP_PHOTOMODE](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_photomode) | KSCAMERA_EXTENDEDPROP_PHOTOMODE 结构包含照片模式下历史记录帧计数的属性数据。 |
| [KSCAMERA_EXTENDEDPROP_PROFILE](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_extendedprop_profile) | KSPROPERTY_CAMERACONTROL_EXTENDED_PROFILE 控件的负载包含 KSCAMERA_EXTENDEDPROP_HEADER + KSCAMERA_EXTENDEDPROP_PROFILE。 |
| [KSCAMERA_EXTENDEDPROP_ROI_CONFIGCAPS](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcaps) | 此结构包含 ROI 控件的功能。 |
| [KSCAMERA_EXTENDEDPROP_ROI_CONFIGCAPSHEADER](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_configcapsheader) | 此结构包含 ROI 功能的标头信息。 |
| [KSCAMERA_EXTENDEDPROP_ROI_EXPOSURE](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_exposure) | 此结构包含公开的 ROI 信息结构。 |
| [KSCAMERA_EXTENDEDPROP_ROI_FOCUS](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_focus) | 此结构包含重点的 ROI 信息结构。 |
| [KSCAMERA_EXTENDEDPROP_ROI_INFO](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_info) | 此结构包含有关 ROI 的信息。 |
| [KSCAMERA_EXTENDEDPROP_ROI_ISPCONTROL](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrol) | 此结构包含 ROI ISP 控制的信息。 |
| [KSCAMERA_EXTENDEDPROP_ROI_ISPCONTROLHEADER](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_ispcontrolheader) | 此结构包含 ROI ISP 控件的标头信息。 |
| [KSCAMERA_EXTENDEDPROP_ROI_WHITEBALANCE](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_roi_whitebalance) | 此结构包含白平衡的 ROI 信息结构。 |
| [KSCAMERA_METADATA_ITEMHEADER](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_itemheader) | 此结构包含由相机驱动程序填充的元数据标头信息。 |
| [KSCAMERA_METADATA_PHOTOCONFIRMATION](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_metadata_photoconfirmation) | 此结构包含由相机驱动程序填充的照片确认元数据信息。 |
| [KSCAMERA_PERFRAMESETTING_CAP_HEADER](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_header) | 此结构包含每帧设置功能的标头信息。 |
| [KSCAMERA_PERFRAMESETTING_CAP_ITEM_HEADER](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_cap_item_header) | 此结构包含每帧设置项的标头信息。 |
| [KSCAMERA_PERFRAMESETTING_CUSTOM_ITEM](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_custom_item) | 此结构包含一个自定义项。 |
| [KSCAMERA_PERFRAMESETTING_FRAME_HEADER](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_frame_header) | 此结构包含每帧设置负载中的帧的标头信息。 |
| [KSCAMERA_PERFRAMESETTING_HEADER](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_header) | 此结构包含每帧设置负载的标头信息。 |
| [KSCAMERA_PERFRAMESETTING_ITEM_HEADER](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kscamera_perframesetting_item_header) | 此结构包含每帧设置项的标头信息。 |
| [KSCAMERA_PROFILE_CONCURRENCYINFO](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_concurrencyinfo) | 照相机中 KSCAMERA_PROFILE_CONCURRENCYINFO 结构的数组。 |
| [KSCAMERA_PROFILE_INFO](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_info) | KSCAMERA_PROFILE_INFO 结构用于唯一标识给定的配置文件。 |
| [KSCAMERA_PROFILE_MEDIAINFO](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_mediainfo) | 此结构包含为每个照相机配置文件提供的相关媒体类型信息。 |
| [KSCAMERA_PROFILE_PININFO](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_kscamera_profile_pininfo) | 此结构指定每个相机驱动程序 pin 的可用媒体类型列表。 |
| [KSDEVICE_PROFILE_INFO](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ksdevice_profile_info) | KSDEVICE_PROFILE_INFO 是一种泛型结构，旨在处理各种设备类型的配置文件信息。 |
| [KSDEVICE_THERMAL_DISPATCH](/windows-hardware/drivers/ddi/ks/ns-ks-_ksdevice_thermal_dispatch) | API 调用中的微型端口驱动程序使用 KSDEVICE_THERMAL_DISPATCH 结构来注册热量通知回调。 此结构包含主动和被动冷却接口的回调函数指针。 |
| [KSPIN_MDL_CACHING_NOTIFICATION](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_mdl_caching_notification) | 此结构由操作系统在内部使用。 |
| [KSPIN_MDL_CACHING_NOTIFICATION32](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_mdl_caching_notification32) | 此结构由操作系统在内部使用。 |
| [KSPROPERTY_STEPPING_LONG](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_long) | KSPROPERTY_STEPPING_LONG 结构定义32位属性的有效值范围。 |
| [KSPROPERTY_STEPPING_LONGLONG](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_longlong) | KSPROPERTY_STEPPING_LONGLONG 结构定义64位属性的有效值范围。 |
| [KSSTREAM_METADATA_INFO](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_metadata_info) | 此结构包含向下传递到驱动程序的元数据信息。 |
| [KSSTREAM_UVC_METADATA](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_uvc_metadata) | KSSTREAM_UVC_METADATA 结构包含帧时间戳信息的开始和结束。 |
| [KSSTREAM_UVC_METADATATYPE_TIMESTAMP](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_uvc_metadatatype_timestamp) | KSSTREAM_UVC_METADATATYPE_TIMESTAMP 结构包含 USB 视频类 (UVC) 时钟和时间戳信息。 |
| [MetadataTimeStamps](/windows/win32/api/mfapi/ns-mfapi-metadatatimestamps) | MetadataTimeStamps 结构描述 MF_CAPTURE_METADATA_FACEROITIMESTAMPS 特性的 blob 格式。 |
| [MF_MDL_SHARED_PAYLOAD_KEY](/windows-hardware/drivers/ddi/ks/ns-ks-_mf_mdl_shared_payload_key) | 此联合由操作系统在内部使用。 |

## <a name="see-also"></a>另请参阅

[适用于 Windows 10 的通用相机驱动程序设计指南](windows-10-technical-preview-camera-drivers-design-guide.md)

[适用于 Windows 10 的通用照相机驱动程序控件](camera-driver-controls.md)

[适用于 Windows 10 的通用照相机驱动程序枚举](camera-driver-enumerations.md)

[适用于 Windows 10 的通用照相机驱动程序功能](camera-driver-functions.md)

[流媒体设备驱动程序参考](/windows-hardware/drivers/ddi/_stream/index)
