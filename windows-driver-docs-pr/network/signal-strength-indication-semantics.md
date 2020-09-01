---
title: 信号强度指示语义
description: 信号强度指示语义
ms.assetid: d28476f8-d567-4fe0-9cb9-4a78d8b0e05b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd15d62560c3dcfec7bc81ce71b4aad0bee89520
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207781"
---
# <a name="signal-strength-indication-semantics"></a>信号强度指示语义


下图显示了在处理信号强度指示时，微型端口驱动程序应遵循的过程。 MB 服务根据当前设备信号强度和设备处于空闲状态的时长调整信号强度报告的阈值和间隔。 通常会在 MB 服务提供的电源管理功能中执行这些操作。 粗体标签是 OID 标识符或事务流控制，而常规文本中的标签是 OID 结构中的重要标志。

![说明用于处理信号强度指示的微型端口驱动程序应遵循的过程的关系图](images/wwansignalstrength.png)

若要更新信号强度指示，请使用以下过程：

1.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

2.  MB 服务将 [OID \_ WWAN \_ 信号 \_ 状态](./oid-wwan-signal-state.md) 发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

3.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN 成功发送 \_ 到 MB 服务。

4.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

5.  MB 服务将 [OID \_ WWAN \_ 信号 \_ 状态](./oid-wwan-signal-state.md) 发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

6.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN 成功发送 \_ 到 MB 服务。

7.  MB 服务将 [OID \_ WWAN \_ 信号 \_ 状态](./oid-wwan-signal-state.md) 发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

8.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN 成功发送 \_ 到 MB 服务。

9.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

 

