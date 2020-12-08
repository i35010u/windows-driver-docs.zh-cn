---
title: 修改转发请求逻辑
description: 修改转发请求逻辑
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1783f2321858bb45dee09ef78da94661690538d7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787129"
---
# <a name="revise-forward-request-logic"></a>修改转发请求逻辑


如果驱动程序无法自行完成请求，则会将请求向下传递到下一个较低的驱动程序。 对于 WDF 驱动程序，下一个较低的驱动程序被视为默认 i/o 目标并由 WDFIOTARGET 对象表示。 若要获取此对象的句柄，驱动程序将调用 [**WdfDeviceGetIoTarget**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetiotarget)。

有关 WDF 驱动程序如何将请求传递到堆栈中的下一个较低驱动程序的信息，请参阅 [转发 I/o 请求](forwarding-i-o-requests.md)。

 

