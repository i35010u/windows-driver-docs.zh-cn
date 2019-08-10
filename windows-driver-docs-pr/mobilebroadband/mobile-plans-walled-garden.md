---
title: 移动计划围墙花园
description: 移动计划围墙花园
ms.assetid: fb1566c6-8d47-4aa9-93f4-415ef7070ac6
keywords:
- Windows Mobile 计划 mobile operators 围墙园
ms.author: windowsdriverdev
ms.date: 07/31/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 8ca5f96d50d318bf31cfc935ed778b515ff969fa
ms.sourcegitcommit: f89a978ee23b9d2f925b13ea56b2c6cd48b4603a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/10/2019
ms.locfileid: "68948132"
---
# <a name="mobile-plans-walled-garden"></a>移动计划围墙花园

移动计划*围墙园*是在客户用完了数据时支持客户的关键所在。 即使没有备用 internet 连接 (如 Wi-fi), 也可以通过它访问 MO 直接门户。 这将使使用者能够购买其他数据计划并管理其订阅。

> [!NOTE]
> 移动计划体系结构不支持围墙园终结点的 IP 范围。 主机名必须用于允许列表。

MO Direct web 门户和`GetBalance` API 终结点也必须属于此围墙园。

## <a name="walled-garden-endpoints"></a>围墙园终结点

只有少量的必需终结点对于最终用户始终是可访问的。 下表定义了围墙园所需的终结点。

| URL | HTTP/HTTPS |
| --- | --- |
| 数据市场<span></span>。 | https |
| 预览版. 数据市场<span></span> | https |
| windows live<span></span>.net | https |
| ctldl. windowsupdate.log<span></span> | http |
| cdp1-信任<span></span>.com | http |
| omniroot<span></span> | http |
| vassg142 omniroot<span></span> | http |
| vassg142. omniroot<span></span> | http |
| <span></span>mscrl | http |
| <span></span>.crl | http |
| msftconnecttest<span></span> | http |
| crl3. digicert<span></span> | http |
| Digicert<span></span> | http |
| <span></span>login .com | http + https |
| storagetos. 数据市场<span></span> | http + https |
| 数据市场<span></span>。 | http + https |
| 数据市场<span></span>(mps) | http + https |
| 暂存数据市场<span></span> | http + https |
| mps-暂存数据市场<span></span> | http + https |
