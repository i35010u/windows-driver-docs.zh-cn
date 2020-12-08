---
title: OID_GEN_VENDOR_DRIVER_VERSION
description: 作为查询，OID_GEN_VENDOR_DRIVER_VERSION OID 指定了供应商分配的微型端口驱动程序的版本号。
keywords:
- OID_GEN_VENDOR_DRIVER_VERSION
ms.date: 11/01/2017
ms.localizationpriority: medium
ms.openlocfilehash: 826a0622c8b15ceeef8945a7bb7a0803affd4671
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813639"
---
# <a name="oid_gen_vendor_driver_version"></a>OID_GEN_VENDOR_DRIVER_VERSION

作为查询，OID_GEN_VENDOR_DRIVER_VERSION OID 指定了供应商分配的微型端口驱动程序的版本号。

不支持设置请求。

## <a name="remarks"></a>备注

返回值的低序位半部分指定次要版本;高阶半部分指定主要版本。

此 OID 对于 NDIS 6.0 和更高的微型端口驱动程序是必需的。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 

