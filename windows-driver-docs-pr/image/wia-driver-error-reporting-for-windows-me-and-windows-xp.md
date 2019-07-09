---
title: Windows Me 和 Windows XP 的 WIA 驱动程序错误报告
description: Windows Me 和 Windows XP 的 WIA 驱动程序错误报告
ms.assetid: 5f696e16-0c22-4d71-98d2-d642e721ac8c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2794b2d3b2d4762a08c0115e2c591a3a1986338
ms.sourcegitcommit: 67aadd2adef4c338b703464c377ae8c910f1f5f9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2019
ms.locfileid: "67622667"
---
# <a name="wia-driver-error-reporting-for-windows-me-and-windows-xp"></a>Windows Me 和 Windows XP 的 WIA 驱动程序错误报告

WIA 微型驱动程序能够以报告到 WIA 应用程序以字符串形式的扩展的错误信息。 收到一个 HRESULT 错误代码后, 一个 WIA 应用程序可以调用**IWiaItemExtras::GetExtendedErrorInfo**方法 （Microsoft Windows SDK 文档中所述），用户可读的字符串说明的详细信息一种错误。 报告的此方法的字符串应本地化为多种语言。

WIA 微型驱动程序应实现以下方法来执行错误报告：

[**IStiUSD::GetLastError** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getlasterror) − WIA 服务调用此方法来检索最近失败的操作的特定于设备的错误代码。

[**IStiUSD::GetLastErrorInfo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/stiusd/nf-stiusd-istiusd-getlasterrorinfo) − WIA 服务调用此方法来检索有关从返回的错误代码的扩展的信息**IStiUSD::GetLastError**方法调用。

[**IWiaMiniDrv::drvGetDeviceErrorStr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr) − WIA 的服务调用此方法以检索描述该错误后继续操作的详细信息或向最终用户指令中的错误的任何可显示字符串。 **IWiaItemExtras::GetExtendedErrorInfo**方法返回此方法将检索到的错误字符串。

WIA 服务要求提供的错误信息如果任一[IWiaMiniDrv COM 接口](iwiaminidrv-com-interface.md)方法将失败。
