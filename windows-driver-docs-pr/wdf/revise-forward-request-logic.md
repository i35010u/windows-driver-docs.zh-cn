---
title: 修改转发请求逻辑
description: 修改转发请求逻辑
ms.assetid: B307AE04-7AA5-453D-9086-CD740617C659
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e57e3a596a206fba678a652b099d8091812836da
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63325166"
---
# <a name="revise-forward-request-logic"></a>修改转发请求逻辑


如果驱动程序无法独自完成请求，它将在堆栈的下层请求传递给下一个较低的驱动程序。 WDF 驱动程序的下一个较低的驱动程序被视为默认 I/O 目标，由 WDFIOTARGET 对象表示。 若要获取此对象，驱动程序调用的句柄[ **WdfDeviceGetIoTarget**](https://msdn.microsoft.com/library/windows/hardware/ff546017)。

WDF 驱动程序如何在堆栈中传递到下一个较低的驱动程序请求有关的信息，请参阅[转发 I/O 请求](forwarding-i-o-requests.md)。

 

 





