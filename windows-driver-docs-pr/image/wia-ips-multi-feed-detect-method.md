---
title: WIA_IPS_MULTI_FEED_DETECT_METHOD
description: WIA_IPS_MULTI_FEED_DETECT_METHOD 属性用于配置设备用来检测多个源条件的方法。
keywords:
- WIA_IPS_MULTI_FEED_DETECT_METHOD 成像设备
topic_type:
- apiref
api_name:
- WIA_IPS_MULTI_FEED_DETECT_METHOD
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 05/17/2019
ms.localizationpriority: medium
ms.openlocfilehash: 6f46c797489681e6de4a128c75da701ca79e301f
ms.sourcegitcommit: 2ddaca0dbaf96076ad54d39ac1e77d91e644de67
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2019
ms.locfileid: "65958675"
---
# <a name="wiaipsmultifeeddetectmethod"></a>WIA\_IPS\_多\_馈送\_检测\_方法

**WIA\_IPS\_多\_源\_检测\_方法**属性用于配置设备用来检测多个源条件的方法。

此属性是初始化和维护的 WIA 微型驱动程序。

属性类型：VT\_I4

有效值：WIA\_PROP\_列表

访问权限：读写

## <a name="remarks"></a>备注

下表中显示此属性的有效值。

| ReplTest1 | 描述 |
| --- | --- |
| WIA_MULTI_FEED_DETECT_ METHOD_LENGTH | 设备测量正在扫描的原始页大小的长度与扫描的页面的长度。 |
| WIA_MULTI_FEED_DETECT_METHOD_OVERLAP | 设备检测重叠扫描的页面。 |

最小化驱动程序支持一组不同的[ **WIA\_IPS\_多\_馈送\_敏感度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-multi-feed-sensitivity)属性值为每个**WIA\_IPS\_多\_馈送\_检测\_方法**属性值。 当同时**WIA\_IP\_多\_源\_检测\_方法**并**WIA\_IP\_多\_馈送\_敏感度**支持的属性，应首先设置 WIA 应用程序**WIA\_IP\_多\_源\_检测\_方法**属性来配置多源的检测方法，然后设置**WIA\_IP\_多\_源\_敏感度**若要配置此检测方法所需区分大小属性的属性。

此属性是仅对送纸器项有效 (WIA\_类别\_送纸器) 和是可选的。 支持的属性时，没有所需的默认值。

## <a name="requirements"></a>要求

| &nbsp; | &nbsp; |
| --- |:--- |
| **标头** | Wiadef.h （包括 Wiadef.h） |
