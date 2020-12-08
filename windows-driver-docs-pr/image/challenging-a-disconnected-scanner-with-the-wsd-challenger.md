---
title: 使用 WSD 质询器质询断开连接的扫描仪
description: 使用 WSD 质询器质询断开连接的扫描仪
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 48f6db46f7334c8e6a187708758e91bd7ee201f1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789907"
---
# <a name="challenging-a-disconnected-scanner-with-the-wsd-challenger"></a>使用 WSD 质询器质询断开连接的扫描仪

> [!IMPORTANT] 
> 已弃用 WSD 争取冠军宝座功能，并且2018中将删除所有与 WSD 争取冠军宝座相关的文档。

当扫描程序重新联机时，web 服务扫描器驱动程序可能会质询断开连接的扫描仪来重新建立与设备的通信。 若要质询已断开的扫描程序，驱动程序使用与 Windows Vista 一起提供 *WSDCHNGR.DLL*) 的 WSD 争取冠军宝座 DLL (。 Windows 映像采集 (WIA) 服务还使用 *WSDCHNGR.DLL* 主动监视所有 WSDScan 扫描程序设备，并使驱动程序能够在设备通信故障后响应挑战。

设备类的挑战由 **WSDCHNGRChallengeDeviceClass** WSD 质询函数启动。 WIA 驱动程序通常不必直接调用此函数，因为 WIA 服务会为所有 WIA 设备调用此函数。

由于 WIA 驱动程序在其支持的设备断开连接后不久就会卸载，因此，驱动程序本身不能保持 *WSDCHNGR.DLL* 加载。 因此，驱动程序无法继续监视 WSD 设备，并且在设备重新联机时无法重新连接到设备。 相反，通过使用 *WSDScan.sys* 内核模式驱动程序安装的 wia 驱动程序可以使用 wia 服务质询设备类，并在卸载驱动程序后，使监视操作的难度更大。

通常，使用 *WSDScan.sys* 的 WIA 驱动程序只使用以下 WSD 争取冠军宝座函数：

<a href="" id="wsdchngrinitialize"></a>**WSDCHNGRInitialize**  
初始化 WIA 驱动程序客户端使用的 WSD 争取冠军宝座接口。 加载驱动程序时调用此函数。

<a href="" id="wsdchngrshutdown"></a>**WSDCHNGRShutdown**  
关闭 WIA 驱动程序客户端使用的 WSD 争取冠军宝座接口。 卸载驱动程序时调用此函数。

**注意**   此关闭发生时，如果设备是 WSDScan 类设备，WIA 服务将继续在卸载驱动程序并终止其 web 服务质询接口后，为设备运行 WSD 质询监视。

 

<a href="" id="wsdchngrregisterdevicetochallenge"></a>**WSDCHNGRRegisterDeviceToChallenge**  
将设备注册为质询。 当驱动程序遇到任何潜在的通信失败后，调用此函数。 同一设备可以多次注册一个质询。 **WSDCHNGRRegisterDeviceToChallenge** \_ 如果成功注册第一个设备，WSDCHNGRRegisterDeviceToChallenge 将返回 S OK。 \_如果为已注册为质询的设备调用此函数，此函数将返回 "FALSE"。

下面的代码示例演示了如何使用这些 WSD 质询函数初始化 WSD 争取冠军宝座，以及如何在发生通信故障后注册 scanner 设备以获得挑战性：

[用于筛选错误代码的宏示例](macro-example-to-filter-error-codes.md)

[演示如何质询可能已断开连接的设备的代码示例](code-example-for-challenging-a-potentially-disconnected-device.md)

[演示如何实现帮助程序方法的代码示例](code-example-for-implementing-helper-methods.md)

有关这些示例中所用的定义和变量的详细信息，请参阅 [示例中使用的定义和变量](definitions-and-variables-used-in-the-examples.md)。

 

 




