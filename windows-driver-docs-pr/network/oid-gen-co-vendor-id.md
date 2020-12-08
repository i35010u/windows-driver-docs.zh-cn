---
title: OID_GEN_CO_VENDOR_ID
description: 本主题介绍) OID_GEN_CO_VENDOR_ID 对象标识符 (OID。
keywords:
- OID_GEN_CO_VENDOR_ID
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb07e6e168cd01513466b6c05e8334ffe995ebaa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839877"
---
# <a name="oid_gen_co_vendor_id"></a>OID_GEN_CO_VENDOR_ID

3字节 IEEE 注册供应商代码，后跟供应商分配的单个字节来标识特定 NIC。

IEEE 代码唯一地标识供应商，与显示在 NIC 硬件地址开头的三个字节相同。

没有 IEEE 注册代码的供应商应该使用值0xFFFFFF。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 

