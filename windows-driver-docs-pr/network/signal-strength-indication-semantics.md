---
title: 信号强度指示语义
description: 信号强度指示语义
ms.assetid: d28476f8-d567-4fe0-9cb9-4a78d8b0e05b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f233869699697fc81b4ed3f74d9aed1f953a62b4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380819"
---
# <a name="signal-strength-indication-semantics"></a>信号强度指示语义


下图显示了过程微型端口驱动程序应遵循为进程信号强度指示。 MB 服务调整强度报告的阈值和间隔，根据当前设备信号强度和长设备已空闲的信号。 通常作为 MB 服务所提供的电源管理功能的一部分执行这些操作。 以粗体显示的标签是 OID 标识符或事务流控制，并在常规文本的标签是 OID 结构中的重要标志。

![说明过程信号强度指示微型端口驱动程序应遵循的过程的关系图](images/wwansignalstrength.png)

若要更新信号强度指示，请使用以下过程：

1.  微型端口驱动程序发送[ **NDIS\_WWAN\_信号\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)到 MB 服务。

2.  MB 服务发送[OID\_WWAN\_信号\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-signal-state)微型端口驱动程序。 微型端口驱动程序会使用临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

3.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_MB 服务的成功。

4.  微型端口驱动程序发送[ **NDIS\_WWAN\_信号\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)到 MB 服务。

5.  MB 服务发送[OID\_WWAN\_信号\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-signal-state)微型端口驱动程序。 微型端口驱动程序会使用临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

6.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_MB 服务的成功。

7.  MB 服务发送[OID\_WWAN\_信号\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-signal-state)微型端口驱动程序。 微型端口驱动程序会使用临时确认进行响应 (NDIS\_状态\_指示\_REQUIRED) 它已收到请求，并且它将发送包含所需的信息在将来的通知。

8.  微型端口驱动程序将发送 NDIS\_状态\_WWAN\_MB 服务的成功。

9.  微型端口驱动程序发送[ **NDIS\_WWAN\_信号\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndiswwan/ns-ndiswwan-_ndis_wwan_signal_state)到 MB 服务。

 

 





