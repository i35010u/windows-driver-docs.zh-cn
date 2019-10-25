---
title: 修改转发请求逻辑
description: 修改转发请求逻辑
ms.assetid: B307AE04-7AA5-453D-9086-CD740617C659
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74f0fe612b2adab674dd4356ea380f4e73b18013
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842203"
---
# <a name="revise-forward-request-logic"></a>修改转发请求逻辑


如果驱动程序无法自行完成请求，则会将请求向下传递到下一个较低的驱动程序。 对于 WDF 驱动程序，下一个较低的驱动程序被视为默认 i/o 目标并由 WDFIOTARGET 对象表示。 若要获取此对象的句柄，驱动程序将调用[**WdfDeviceGetIoTarget**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetiotarget)。

有关 WDF 驱动程序如何将请求传递到堆栈中的下一个较低驱动程序的信息，请参阅[转发 I/o 请求](forwarding-i-o-requests.md)。

 

 





