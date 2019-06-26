---
title: 设置端口身份验证参数
description: 设置端口身份验证参数
ms.assetid: 88ac8229-d1d5-4287-8b5d-3a7b9b1f2e89
keywords:
- 端口 WDK NDIS OID 请求
- NDIS 端口 WDK，OID 请求
- OID 请求 WDK NDIS 端口
- 身份验证参数 WDK NDIS 端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0b5f4136862c496ce934dd0d395b5ecfeeb9dab1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67375143"
---
# <a name="setting-port-authentication-parameters"></a>设置端口身份验证参数





使用 NDIS 和基础驱动程序[OID\_代\_端口\_身份验证\_参数](https://docs.microsoft.com/windows-hardware/drivers/network/oid-gen-port-authentication-parameters)OID 设置请求以设置 NDIS 端口的当前状态。 支持 NDIS 端口的微型端口驱动程序必须支持此 OID。

如果集请求成功，微型端口驱动程序使用的接收端口方向、 端口控件状态，并进行身份验证中的状态[ **NDIS\_端口\_身份验证\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters)结构。

微型端口应生成[ **NDIS\_状态\_端口\_状态**](https://docs.microsoft.com/windows-hardware/drivers/network/ndis-status-port-state)状态指示通知的任何状态更改的基础驱动程序。

 

 





