---
title: 电源管理次要 IRP
description: 电源管理次要 IRP
ms.date: 08/12/2017
ms.assetid: 8af0609f-168b-4455-aae8-1a3c9e40ed47
ms.localizationpriority: medium
ms.openlocfilehash: 99e1a345ade8e93329d94bcb03568d644d42e6ca
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187737"
---
# <a name="power-management-minor-irps"></a>电源管理次要 IRP





所有电源 Irp 都具有主要的代码 [**IRP \_ MJ \_ 功能**](irp-mj-power.md) 和以下次要代码之一，指示特定电源管理请求：

[**IRP \_ MN \_ 幂 \_ 序列**](irp-mn-power-sequence.md)

[**IRP \_ MN \_ 查询 \_ 能力**](irp-mn-query-power.md)

[**IRP \_ MN \_ 设置 \_ 电源**](irp-mn-set-power.md)

[**IRP \_ MN \_ 等待 \_ 唤醒**](irp-mn-wait-wake.md)

本部分按字母顺序提供单个 Irp 的参考信息。 有关何时发送 Irp 以及驱动程序应如何处理它们的详细信息，请参阅 [电源管理](./introduction-to-power-management.md)。 "电源管理" 部分还介绍了电源管理和术语。

 

