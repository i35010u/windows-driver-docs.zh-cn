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
ms.openlocfilehash: 09cb15313092b834341bbe840f576ade3b36a781
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546509"
---
# <a name="setting-port-authentication-parameters"></a>设置端口身份验证参数





使用 NDIS 和基础驱动程序[OID\_代\_端口\_身份验证\_参数](https://msdn.microsoft.com/library/windows/hardware/ff569623)OID 设置请求以设置 NDIS 端口的当前状态。 支持 NDIS 端口的微型端口驱动程序必须支持此 OID。

如果集请求成功，微型端口驱动程序使用的接收端口方向、 端口控件状态，并进行身份验证中的状态[ **NDIS\_端口\_身份验证\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566788)结构。

微型端口应生成[ **NDIS\_状态\_端口\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567415)状态指示通知的任何状态更改的基础驱动程序。

 

 





