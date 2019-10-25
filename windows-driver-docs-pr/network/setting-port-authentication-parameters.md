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
ms.openlocfilehash: f9d87dd9bf52821b4dedc280b6d32cfc5a6bb036
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841937"
---
# <a name="setting-port-authentication-parameters"></a>设置端口身份验证参数





NDIS 驱动程序和过量驱动程序使用[oid\_代\_端口\_身份验证\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-authentication-parameters)OID 设置请求以设置 NDIS 端口的当前状态。 支持 NDIS 端口的微型端口驱动程序必须支持此 OID。

如果设置请求成功，则微型端口驱动程序使用接收端口方向、端口控制状态，并通过[**NDIS\_端口\_AUTHENTICATION\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters)结构来验证状态。

微型端口应生成一个[**NDIS\_状态\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)指示，通知过量驱动程序任何状态更改。

 

 





