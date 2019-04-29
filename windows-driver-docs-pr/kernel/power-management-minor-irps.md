---
title: 电源管理次要 IRP
description: 电源管理次要 IRP
ms.date: 08/12/2017
ms.assetid: 8af0609f-168b-4455-aae8-1a3c9e40ed47
ms.localizationpriority: medium
ms.openlocfilehash: c041e8a4b45465530a3cf8d23f4cdc93f1756fe0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369151"
---
# <a name="power-management-minor-irps"></a>电源管理次要 IRP





所有 power Irp 都具有重大的代码[ **IRP\_MJ\_POWER** ](irp-mj-power.md)和以下小代码，指示特定电源管理请求之一：

[**IRP\_MN\_POWER\_SEQUENCE**](irp-mn-power-sequence.md)

[**IRP\_MN\_查询\_电源**](irp-mn-query-power.md)

[**IRP\_MN\_SET\_POWER**](irp-mn-set-power.md)

[**IRP\_MN\_WAIT\_WAKE**](irp-mn-wait-wake.md)

本部分提供有关各个 Irp 按字母顺序参考信息。 有关详细信息，有关何时 Irp 发送和驱动程序应如何处理它们，请参阅[电源管理](https://msdn.microsoft.com/library/windows/hardware/ff547131)。 电源管理部分还包括电源管理和术语的常规介绍。

 

 




