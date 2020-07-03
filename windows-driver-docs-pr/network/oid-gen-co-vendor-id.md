---
title: OID_GEN_CO_VENDOR_ID
description: 本主题介绍 OID_GEN_CO_VENDOR_ID 对象标识符（OID）。
ms.assetid: ec8d47e4-0b2f-4ca8-9227-330030a2ede5
keywords:
- OID_GEN_CO_VENDOR_ID
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: eb4c51320642946d336a806d553cffa33f5fc5d4
ms.sourcegitcommit: 82a9be3b3584f991e5121f8f46a972e04185fa52
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2020
ms.locfileid: "85917019"
---
# <a name="oid_gen_co_vendor_id"></a>OID_GEN_CO_VENDOR_ID

3字节 IEEE 注册供应商代码，后跟供应商分配的单个字节来标识特定 NIC。

IEEE 代码唯一地标识供应商，与显示在 NIC 硬件地址开头的三个字节相同。

没有 IEEE 注册代码的供应商应该使用值0xFFFFFF。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的**标头**： Ntddndis （包括 Ndis .h）

