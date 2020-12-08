---
title: 从 COPP 函数返回错误代码
description: 从 COPP 函数返回错误代码
keywords:
- 复制保护 WDK COPP，错误代码
- 视频复制保护 WDK COPP，错误代码
- COPP WDK DirectX VA，错误代码
- 受保护的视频 WDK COPP，错误代码
- 错误代码 WDK COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c8cfbf84734cf13505c2e32a00c672c2bcf6c9a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824167"
---
# <a name="returning-error-codes-from-copp-functions"></a>从 COPP 函数返回错误代码


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

[COPP DDI](sample-functions-for-copp.md)可以返回以下类型的错误代码：

-   *Winerror.h* 头文件中定义的错误代码，对所有 Windows 应用程序都是通用的。 这些 Windows 错误代码以 E 前缀开头 \_ 。

-   在 *ddraw* 头文件中定义的错误代码，并且对于 DirectDraw 是唯一的。 这些 DirectDraw 错误代码以 DDERR 前缀开头 \_ 。

没有错误代码对 COPP DDI 是唯一的。

实现 COPP DDI 时，应将 Windows 错误代码的使用限制为以下各项：

-   E \_ 意外

    显示驱动程序处于无效状态。 例如，在 [*COPPKeyExchange*](./coppkeyexchange.md)函数之前调用了 [*COPPSequenceStart*](./coppsequencestart.md)函数。

-   E \_ INVALIDARG

    传递给驱动程序的输入参数无效。

-   E \_ 指针

    应指向有效地址的输出参数为 **NULL**。

COPP DDI 可以返回 E \_ FAIL 和 DDERR \_ 一般错误代码; 但是，由于它们并不表示导致错误的原因，因此不建议使用它们。

每个 COPP 函数的 "备注" 部分指定 \_ COPP 函数可以报告的 DDERR 错误代码。 不应要求 COPP DDI 返回任何其他 DDERR \_ 错误代码。

在将视频微型端口驱动程序中的 COPP DDI 传播到显示驱动程序时，不应使用来自 [**EngDeviceIoControl**](/windows/win32/api/winddi/nf-winddi-engdeviceiocontrol) 函数的返回值，因为 Windows 内核会将从 IOCTL 返回的错误值处理到 **EngDeviceIoControl**。 相反，应通过 **EngDeviceIoControl** 的 *lpInBuffer* 参数传递错误消息。 有关详细信息，请参阅 [从显示器驱动程序调用 COPP DDI](calling-the-copp-ddi-from-the-display-driver.md) 和 [COPP 视频微型端口驱动程序模板](copp-video-miniport-driver-template.md) 中的示例代码和 [执行 COPP 操作](performing-copp-operations-example.md)。

 

