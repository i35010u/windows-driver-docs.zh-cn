---
title: WIA_IPS_MULTI_FEED_DETECT_METHOD
description: WIA_IPS_MULTI_FEED_DETECT_METHOD 属性用于配置设备用于检测多个源条件的方法。
keywords:
- WIA_IPS_MULTI_FEED_DETECT_METHOD 图像设备
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
ms.openlocfilehash: d2f84d7a3863925ac12da1fc091dc5f5b20443c3
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191491"
---
# <a name="wia_ips_multi_feed_detect_method"></a>WIA \_ IPS \_ 多 \_ 源 \_ 检测 \_ 方法

" **WIA \_ IPS \_ 多 \_ 源 \_ 检测 \_ 方法** " 属性用于配置设备用于检测多个源条件的方法。

此属性由 WIA 迷你驱动程序初始化和维护。

属性类型： VT \_ I4

有效值： WIA 内容 \_ \_ 列表

访问权限：读写

## <a name="remarks"></a>备注

下表显示了此属性的有效值。

| Value | 描述 |
| --- | --- |
| WIA_MULTI_FEED_DETECT_ METHOD_LENGTH | 设备测量扫描页面的长度，其长度为正在扫描的原始页面大小的长度。 |
| WIA_MULTI_FEED_DETECT_METHOD_OVERLAP | 设备检测到重叠的扫描页面。 |

对于每个**wia \_ ips \_ 多 \_ 源 \_ 检测 \_ 方法**属性值，小型驱动程序可以支持一组不同的[**wia \_ ips \_ 多 \_ 源 \_ 敏感度**](./wia-ips-multi-feed-sensitivity.md)属性值。 当 **wia \_ ips \_ 多 \_ 源 \_ 检测 \_ 方法** 和 **wia \_ ips 多源 \_ \_ \_ 敏感度** 属性均受支持时，WIA 应用程序应该首先设置 " **wia \_ ips \_ 多 \_ 源 \_ 检测 \_ 方法** " 属性以配置多源检测方法，然后设置 " **wia \_ ips \_ 多 \_ 源 \_ 敏感度** " 属性以配置此检测方法的所需敏感度。

此属性仅对 (WIA 类别送纸器) 的进纸器项有效 \_ \_ ，并且是可选的。 如果支持该属性，则不需要默认值。

## <a name="requirements"></a>要求

| &nbsp; | &nbsp; |
| --- |:--- |
| **标头** | Wiadef (包含 Wiadef)  |