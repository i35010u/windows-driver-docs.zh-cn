---
title: 设置端口身份验证参数
description: 设置端口身份验证参数
ms.assetid: 88ac8229-d1d5-4287-8b5d-3a7b9b1f2e89
keywords:
- 端口 WDK NDIS，OID 请求
- NDIS 端口 WDK，OID 请求
- OID 请求 WDK NDIS 端口
- 身份验证参数 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88c84028fd5164ae4f5fcc933c8782621652048d
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214440"
---
# <a name="setting-port-authentication-parameters"></a>设置端口身份验证参数





NDIS 和过量驱动程序使用 [oid \_ GEN \_ 端口 \_ 身份验证 \_ 参数](./oid-gen-port-authentication-parameters.md) OID 设置请求，以设置 NDIS 端口的当前状态。 支持 NDIS 端口的微型端口驱动程序必须支持此 OID。

如果设置请求成功，微型端口驱动程序将使用接收端口方向、端口控制状态以及从 [**NDIS \_ 端口 \_ 身份验证 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters) 结构验证状态。

微型端口应生成 [**NDIS \_ 状态 \_ 端口 \_ 状态**](./ndis-status-port-state.md) 状态指示，以通知过量驱动程序任何状态更改。

 

