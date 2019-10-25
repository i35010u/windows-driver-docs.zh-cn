---
title: Windows Me 和 Windows XP 的 WIA 驱动程序错误报告
description: Windows Me 和 Windows XP 的 WIA 驱动程序错误报告
ms.assetid: 5f696e16-0c22-4d71-98d2-d642e721ac8c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcbd156d288429edc6a5c5b69d8b7e31b3fb381f
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840709"
---
# <a name="wia-driver-error-reporting-for-windows-me-and-windows-xp"></a>Windows Me 和 Windows XP 的 WIA 驱动程序错误报告

WIA 微型驱动程序能够以字符串形式向 WIA 应用程序报告扩展的错误信息。 接收到 HRESULT 错误代码后，WIA 应用程序可以调用**IWiaItemExtras：： GetExtendedErrorInfo**方法（如 Microsoft Windows SDK 文档中所述）来查看描述错误详细信息的用户可读字符串。 此方法报告的字符串应本地化为多种语言。

WIA 微型驱动程序应实现以下方法来执行错误报告：

[**IStiUSD：： GetLastError**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getlasterror) − WIA 服务调用此方法来检索设备特定的错误代码，以获得最近的失败操作。

[**IStiUSD：： GetLastErrorInfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getlasterrorinfo) − WIA 服务调用此方法来检索有关从**IStiUSD：： GetLastError**方法调用返回的错误代码的扩展信息。

[**IWiaMiniDrv：:D rvgetdeviceerrorstr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr) − WIA 服务调用此方法来检索任何详细描述错误的可显示字符串，或在出现错误后如何继续操作的说明。 **IWiaItemExtras：： GetExtendedErrorInfo**方法返回此方法检索到的错误字符串。

如果任何[IWIAMINIDRV COM 接口](iwiaminidrv-com-interface.md)方法失败，WIA 服务将请求提供错误信息。
