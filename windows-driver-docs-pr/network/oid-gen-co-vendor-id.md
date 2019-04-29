---
title: OID_GEN_CO_VENDOR_ID
description: 本主题介绍 OID_GEN_CO_VENDOR_ID 对象标识符 (OID)。
ms.assetid: ec8d47e4-0b2f-4ca8-9227-330030a2ede5
keywords:
- OID_GEN_CO_VENDOR_ID
ms.date: 11/02/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47e03f2ae75759b27d09d33edcc463fa6de7097a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355715"
---
# <a name="oidgencovendorid"></a>OID_GEN_CO_VENDOR_ID

3 字节 IEEE 注册供应商代码后, 跟一个字节的供应商用来标识特定的 nic。

IEEE 代码唯一标识供应商并等同于使其不显示在 NIC 硬件地址开头的三个字节。

未使用 IEEE 注册的代码的供应商应使用 0xFFFFFF 的值。

## <a name="requirements"></a>要求

| | |
| --- | --- |
| Version | Windows Vista 及更高版本 |
| Header | Ntddndis.h （包括 Ndis.h） |

