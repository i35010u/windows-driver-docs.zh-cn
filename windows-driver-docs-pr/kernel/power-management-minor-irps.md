---
title: 电源管理次要 IRP
description: 电源管理次要 IRP
ms.date: 08/12/2017
ms.localizationpriority: medium
ms.openlocfilehash: d57b8b6b7cad2f9d2857815f40fceb06d80b4807
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803793"
---
# <a name="power-management-minor-irps"></a>电源管理次要 IRP





所有电源 Irp 都具有主要的代码 [**IRP \_ MJ \_ 功能**](irp-mj-power.md) 和以下次要代码之一，指示特定电源管理请求：

[**IRP \_ MN \_ 幂 \_ 序列**](irp-mn-power-sequence.md)

[**IRP \_ MN \_ 查询 \_ 能力**](irp-mn-query-power.md)

[**IRP \_ MN \_ 设置 \_ 电源**](irp-mn-set-power.md)

[**IRP \_ MN \_ 等待 \_ 唤醒**](irp-mn-wait-wake.md)

本部分按字母顺序提供单个 Irp 的参考信息。 有关何时发送 Irp 以及驱动程序应如何处理它们的详细信息，请参阅 [电源管理](./introduction-to-power-management.md)。 "电源管理" 部分还介绍了电源管理和术语。

 

