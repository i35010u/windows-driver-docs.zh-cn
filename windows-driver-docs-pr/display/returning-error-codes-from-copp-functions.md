---
title: 从 COPP 函数返回错误代码
description: 从 COPP 函数返回错误代码
ms.assetid: a42fba73-59b2-4106-ba2b-9e96cd8524c8
keywords:
- 复制保护 WDK COPP，错误代码
- 视频复制保护 WDK COPP，错误代码
- COPP WDK DirectX VA，错误代码
- 受保护视频 WDK COPP，错误代码
- 错误代码 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f3ccfeb986853dff58b2c9fe4b526412aef069f
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67365622"
---
# <a name="returning-error-codes-from-copp-functions"></a>从 COPP 函数返回错误代码


**本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。**

[COPP DDI](sample-functions-for-copp.md)可以返回以下类型的错误代码：

-   在中定义的错误代码*winerror.h*标头文件和都普遍适用于所有 Windows 应用程序。 这些 Windows 错误代码开头 E\_前缀。

-   在中定义的错误代码*ddraw.h*标头文件和都唯一的 DirectDraw。 这些 DirectDraw 错误代码开头 DDERR\_前缀。

没有错误代码是唯一的 COPP DDI。

在实现 COPP DDI 时，应与以下来限制 Windows 错误代码的使用情况：

-   E\_意外的

    显示驱动程序处于无效状态。 例如， [ *COPPSequenceStart* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppsequencestart)函数调用之前[ *COPPKeyExchange* ](https://docs.microsoft.com/windows-hardware/drivers/display/coppkeyexchange)函数。

-   E\_INVALIDARG

    传递给驱动程序的输入的参数均无效。

-   E\_指针

    输出参数，应指向有效的地址，该参数是**NULL**。

COPP DDI 可返回 E\_失败，而且 DDERR\_泛型错误代码; 但是，因为它们不指示错误的原因，不建议其使用。

每个 COPP 函数的备注部分指定 DDERR\_ COPP 函数可以报告的错误代码。 COPP DDI 不应需要返回任何其他 DDERR\_错误代码。

传播 COPP DDI 微型端口驱动程序中显示驱动程序到错误信息时, 不应使用的返回值[ **EngDeviceIoControl** ](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeviceiocontrol)函数，因为 Windows内核操作从到 IOCTL 返回的错误值**EngDeviceIoControl**。 相反，应传递错误信息*lpInBuffer*的参数**EngDeviceIoControl**。 有关详细信息，请参阅[从显示器驱动程序调用 COPP DDI](calling-the-copp-ddi-from-the-display-driver.md)和中的代码示例[COPP 视频微型端口驱动程序模板](copp-video-miniport-driver-template.md)并[执行 COPP 操作](performing-copp-operations-example.md)。

 

 





