---
title: MB 信号强度操作
description: MB 信号强度操作
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: db4cb56cf5668680ddb591e9a79bf3c5928d928a
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248210"
---
# <a name="mb-signal-strength-operations"></a>MB 信号强度操作


本主题介绍用于报告信号强度的操作。

这些操作需要访问网络提供程序，而不是 (SIM 卡) 的订阅服务器标识模块。

请注意，在基于 GSM 的设备情况下，微型端口驱动程序只应在已成功向网络提供商注册了微型端口驱动程序后发送信号强度通知。 对于基于 CDMA 的设备，微型端口驱动程序可以在微型端口驱动程序成功注册到网络提供程序之前发送信号强度通知。

## <a name="signal-strength-indication-semantics"></a>信号强度指示语义


下图显示了在处理信号强度指示时，微型端口驱动程序应遵循的过程。 MB 服务根据当前设备信号强度和设备处于空闲状态的时长调整信号强度报告的阈值和间隔。 通常会在 MB 服务提供的电源管理功能中执行这些操作。 粗体标签为 OID 标识符或事务流控制。 常规文本中的标签是 OID 结构中的重要标志。

![说明用于处理信号强度指示的微型端口驱动程序应遵循的过程的关系图](images/wwansignalstrength.png)

若要更新信号强度指示，请使用以下过程：

1.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

2.  MB 服务将 [OID \_ WWAN \_ 信号 \_ 状态](oid-wwan-signal-state.md) 发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

3.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN 成功发送 \_ 到 MB 服务。

4.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

5.  MB 服务将 [OID \_ WWAN \_ 信号 \_ 状态](oid-wwan-signal-state.md) 发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

6.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN 成功发送 \_ 到 MB 服务。

7.  MB 服务将 [OID \_ WWAN \_ 信号 \_ 状态](oid-wwan-signal-state.md) 发送到微型端口驱动程序。 微型端口驱动程序使用临时确认响应 (需要的 NDIS \_ 状态 \_ 指示 \_) 它已收到请求，并将在将来发送包含所需信息的通知。

8.  微型端口驱动程序将 NDIS \_ 状态 \_ WWAN 成功发送 \_ 到 MB 服务。

9.  微型端口驱动程序将 [**NDIS \_ WWAN \_ 信号 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state) 发送到 MB 服务。

 

