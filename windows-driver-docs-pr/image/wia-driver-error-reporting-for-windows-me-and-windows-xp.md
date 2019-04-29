---
title: Windows Me 和 Windows XP 的 WIA 驱动程序错误报告
description: Windows Me 和 Windows XP 的 WIA 驱动程序错误报告
ms.assetid: 5f696e16-0c22-4d71-98d2-d642e721ac8c
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88596293ea08d745d11fece45f6b3cb5202f6ed9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366889"
---
# <a name="wia-driver-error-reporting-for-windows-me-and-windows-xp"></a>Windows Me 和 Windows XP 的 WIA 驱动程序错误报告





WIA 微型驱动程序能够以报告到 WIA 应用程序以字符串形式的扩展的错误信息。 收到一个 HRESULT 错误代码后, 一个 WIA 应用程序可以调用**IWiaItemExtras::GetExtendedErrorInfo**方法 （Microsoft Windows SDK 文档中所述），用户可读的字符串说明的详细信息一种错误。 报告的此方法的字符串应本地化为多种语言。

WIA 微型驱动程序应实现以下方法来执行错误报告：

[**IStiUSD::GetLastError** ](https://msdn.microsoft.com/library/windows/hardware/ff543818) − WIA 服务调用此方法来检索最近失败的操作的特定于设备的错误代码。

[**IStiUSD::GetLastErrorInfo** ](https://msdn.microsoft.com/library/windows/hardware/ff543820) − WIA 服务调用此方法来检索有关从返回的错误代码的扩展的信息**IStiUSD::GetLastError**方法调用。

[**IWiaMiniDrv::drvGetDeviceErrorStr** ](https://msdn.microsoft.com/library/windows/hardware/ff543982) − WIA 的服务调用此方法以检索描述该错误后继续操作的详细信息或向最终用户指令中的错误的任何可显示字符串。 **IWiaItemExtras::GetExtendedErrorInfo**方法返回此方法将检索到的错误字符串。

WIA 服务要求提供的错误信息如果任一[IWiaMiniDrv COM 接口](iwiaminidrv-com-interface.md)方法将失败。

 

 




