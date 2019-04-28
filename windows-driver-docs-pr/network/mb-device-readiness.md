---
title: MB 设备就绪状态
description: MB 设备就绪状态
ms.assetid: 67a67ff7-dcff-4aec-bea9-7b1be9593649
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95f83da274cae07e6a886ab706d852a48c8c1afd
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63343409"
---
# <a name="mb-device-readiness"></a>MB 设备就绪状态


本主题介绍的过程，以确保 MB 设备可访问，并且准备好之前 MB 服务将继续安装程序的数据连接到用于与网络相关的活动。 设备已准备好使用已激活用户订阅和订阅服务器相关信息存储到设备或用户识别模块 （SIM 卡）

MB 服务会假定微型端口驱动程序会自动初始化其 MB 设备的硬件 （单选堆栈、 SIM 卡或等效的电路） 系统已加载，而无需等待来自服务的任何指令之后。

微型端口驱动程序设置到其 MB 设备的初始就绪状态**WwanReadyStateOff**。 因为它们继续进行初始化，微型端口驱动程序必须发送事件通知来告知对其设备就绪状态的更改 MB 服务。

如果他们会遇到任何错误条件，微型端口驱动程序必须停止初始化过程。 清除错误条件后，微型端口驱动程序可以继续初始化过程到其设备已达到**WwanReadyStateInitialized**就绪状态。

某些错误情况的示例如下：

-   如果设备需要 SIM 卡并且微型端口驱动程序检测到任何 SIM 卡是否存在，微型端口驱动程序必须发送**WwanReadyStateSimNotInserted**就绪状态事件通知和微型端口驱动程序必须保留在的中状态，直到用户将 SIM 卡插入到设备。

-   如果设备需要 SIM 卡，并且微型端口驱动程序不能读取已插入 SIM 卡 （例如，U RIM 插入到基于 GSM 的设备或 USIM 插入到基于 CDMA 的设备） 或 SIM 卡 （例如，不符合设备 3 个 G USIM 插入到 2g 设备无法解释 USIM 格式），微型端口驱动程序必须发送**WwanReadyStateBadSim**就绪状态事件通知和微型端口驱动程序必须保持该状态直到用户将正确的 SIM 卡插入到设备。

-   如果在设备锁定 pin （适用于使用 SIM 卡的设备） 或通过密码 （适用于不使用 SIM 卡的设备），可防止进一步设备初始化进度，微型端口驱动程序必须发送**WwanReadyStateDeviceLocked**就绪状态事件通知和微型端口驱动程序必须保持该状态直到用户输入正确的 PIN 或密码。

-   微型端口驱动程序微型端口驱动程序检测到需要服务激活以继续操作，如果必须发送**WwanReadyStateNotActivated**就绪状态事件通知，并且它必须保持该状态直到已将服务激活。 这是为基于 CDMA 的设备在北美的典型行为。

-   微型端口驱动程序微型端口驱动程序在遇到故障不是在前面提到，如果必须发送**WwanReadyStateFailure**就绪状态事件通知，并且它必须保持该状态直到问题已得到标识和更正。

请注意 MB 服务不会假设微型端口驱动程序可以检测这些错误。 也不会在服务假设的微型端口驱动程序检测这些错误条件的顺序。 但是，它是实现前面列出的顺序错误情况。

微型端口驱动程序将发送之前**WwanReadyStateInitialized**就绪状态事件通知，直到确定并更正问题，该服务将无法继续任何深一层与网络相关的活动。 但是，该服务仍可能会向微型端口驱动程序发送 Oid。

微型端口驱动程序不需要等待才能报告之前准备就绪的短信子系统**WwanReadyStateInitialized**就绪状态。 相反，微型端口驱动程序应该发送一个单独[OID\_WWAN\_SMS\_配置](https://msdn.microsoft.com/library/windows/hardware/ff569837)通知时的短信子系统已准备好发送和接收 SMS 消息。

### <a name="emergency-mode-support"></a>紧急模式下支持

如果微型端口驱动程序表明它支持紧急调用服务在处理[OID\_WWAN\_准备\_信息](https://msdn.microsoft.com/library/windows/hardware/ff569833)微型端口驱动程序必须设置**EmergencyMode**的成员[ **WWAN\_准备\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff571226)结构**WwanEmergencyModeOn**。 在这种情况下，微型端口驱动程序应继续注册通知发送到 MB 服务，但该服务将不会调用任何自动与配置相关的功能。

微型端口驱动程序可以指定它们甚至在其中检测到，SIM 不再有效，可能是因为该订阅未付款，或者服务已被停用，因为该设备已报告被盗的情况下支持紧急调用服务。

有关设备的准备情况的详细信息，请参阅[OID\_WWAN\_准备\_信息](https://msdn.microsoft.com/library/windows/hardware/ff569833)。

 

 





