---
title: 具有挑战性的断开连接与 WSD 占领扫描仪
description: 具有挑战性的断开连接与 WSD 占领扫描仪
ms.assetid: f938a235-0360-43f9-9f84-6b9cb6ca9245
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0da63b43d71af20550fab340e97cc790ccdd6607
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547953"
---
# <a name="challenging-a-disconnected-scanner-with-the-wsd-challenger"></a>具有挑战性的断开连接与 WSD 占领扫描仪

> [!IMPORTANT] 
> WSD 占领功能已弃用，将在 2018年中删除所有与 WSD 占领相关文档。

Web 服务扫描程序驱动程序可以质询已断开连接的扫描程序以与设备重新建立通信，扫描程序重新联机时。 质询已断开连接的扫描程序，则驱动程序使用 WSD 占领 DLL (*WSDCHNGR.DLL*) 提供与 Windows Vista。 Windows 图像采集 (WIA) 服务还使用*WSDCHNGR.DLL*来主动监视所有 WSDScan 扫描程序设备并启用驱动程序来响应设备通信发生故障之后的一项挑战。

由启动某类设备的难题**WSDCHNGRChallengeDeviceClass** WSD 质询函数。 WIA 驱动程序通常无需直接调用此函数，因为 WIA 服务进行的调用 WIA 的所有设备。

它支持的设备已断开连接后不久，WIA 驱动程序被卸载，因为不能保持驱动程序本身*WSDCHNGR.DLL*加载。 该驱动程序，因此，无法继续监视 WSD 具有挑战性，并且无法重新连接到设备重新联机时。 相反，通过使用安装的 WIA 驱动程序*WSDScan.sys*内核模式驱动程序可以使用 WIA 服务质询的设备类和启用的具有挑战性的监视以卸载该驱动程序后继续。

通常情况下，一个正在使用的 WIA 驱动程序才能*WSDScan.sys*使用仅以下 WSD 占领函数：

<a href="" id="wsdchngrinitialize"></a>**WSDCHNGRInitialize**  
初始化 WIA 驱动程序客户端使用的 WSD 占领接口。 加载驱动程序，请调用此函数。

<a href="" id="wsdchngrshutdown"></a>**WSDCHNGRShutdown**  
关闭 WIA 驱动程序客户端使用的 WSD 占领接口。 卸载该驱动程序时，请调用此函数。

**请注意**   WIA 服务在此关闭情况下，如果设备是 WSDScan 类设备，继续运行 WSD 质询监视设备后驱动程序已被卸载并终止其 web 服务的挑战接口.

 

<a href="" id="wsdchngrregisterdevicetochallenge"></a>**WSDCHNGRRegisterDeviceToChallenge**  
注册设备质询。 调用此函数后，驱动程序在遇到任何潜在的通信失败。 同一个设备可以多次注册质询。 **WSDCHNGRRegisterDeviceToChallenge**返回 S\_如果成功注册第一台设备，确定。 此函数将返回 S\_FALSE 时调用的设备的已注册为又一个难题。

下面的代码示例演示如何使用这些 WSD 质询函数来初始化 WSD 占领以及如何注册适用于潜在的通信发生故障后具有挑战性的扫描程序设备：

[若要筛选错误代码的宏示例](macro-example-to-filter-error-codes.md)

[针对具有挑战性可能断开连接的设备的代码示例](code-example-for-challenging-a-potentially-disconnected-device.md)

[实现帮助器方法的代码示例](code-example-for-implementing-helper-methods.md)

有关定义和这些示例中使用的变量的详细信息，请参阅[定义和示例中使用变量](definitions-and-variables-used-in-the-examples.md)。

 

 




