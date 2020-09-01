---
title: 直接从用户模式查询微型端口驱动程序
description: 直接从用户模式查询微型端口驱动程序
ms.assetid: e0d153bf-0e50-47bc-b4e2-10f04c532b99
keywords:
- 用户模式驱动程序查询 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 543e8e0da7f2cd9db4418f0a1d773be12ae88446
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215134"
---
# <a name="querying-a-miniport-driver-directly-from-user-mode"></a>直接从用户模式查询微型端口驱动程序





应用程序可以使用 [**IOCTL \_ NDIS \_ 查询 \_ 全局 \_ 统计**](/previous-versions/windows/hardware/network/ff548975(v=vs.85)) 信息直接从微型端口驱动程序的 NIC 中查询信息。 在此操作中，应用程序可以使用微型端口驱动程序支持的任何查询 OID。

 

