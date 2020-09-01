---
title: MB 信号强度操作
description: MB 信号强度操作
ms.assetid: 489299d0-29c5-4885-ae68-f3d0f42bd201
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d290648bf18ffded0e1d5af3c86fa9dba151d994
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207261"
---
# <a name="mb-signal-strength-operations"></a>MB 信号强度操作


本主题介绍用于报告信号强度的操作。

这些操作需要访问网络提供程序，而不是 (SIM 卡) 的订阅服务器标识模块。

请注意，在基于 GSM 的设备情况下，微型端口驱动程序只应在已成功向网络提供商注册了微型端口驱动程序后发送信号强度通知。 对于基于 CDMA 的设备，微型端口驱动程序可以在微型端口驱动程序成功注册到网络提供程序之前发送信号强度通知。

有关信号强度操作的详细信息，请参阅 [OID \_ WWAN \_ 信号 \_ 状态](./oid-wwan-signal-state.md)。

 

