---
title: OID_GEN_VENDOR_DRIVER_VERSION
description: 作为查询，OID_GEN_VENDOR_DRIVER_VERSION OID 指定了供应商分配的微型端口驱动程序的版本号。
ms.assetid: 37CB6A21-9AF2-49BF-AFBA-868C0C6C5383
keywords:
- OID_GEN_VENDOR_DRIVER_VERSION
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: f25991dd8620d6372252e4526f419606910c4c20
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917007"
---
# <a name="oid_gen_vendor_driver_version"></a>OID_GEN_VENDOR_DRIVER_VERSION

作为查询，OID_GEN_VENDOR_DRIVER_VERSION OID 指定了供应商分配的微型端口驱动程序的版本号。

不支持设置请求。

## <a name="remarks"></a>备注

返回值的低序位半部分指定次要版本;高阶半部分指定主要版本。

此 OID 对于 NDIS 6.0 和更高的微型端口驱动程序是必需的。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

