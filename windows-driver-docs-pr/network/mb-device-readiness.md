---
title: MB 设备就绪状态
description: MB 设备就绪状态
ms.assetid: 67a67ff7-dcff-4aec-bea9-7b1be9593649
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0255f56b6755a455a4697cdc555c028a655e275
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72844293"
---
# <a name="mb-device-readiness"></a>MB 设备就绪状态


本主题介绍了在 MB 服务继续设置数据连接之前确保 MB 设备可用于网络相关活动的步骤。 已激活用户订阅和存储到设备或订阅服务器标识模块（SIM 卡）的订户相关信息时，设备可供使用

MB 服务假定微型端口驱动程序在系统加载它后自动初始化其 MB 设备的硬件（收音机 stack、SIM 卡或等效电路），而无需等待来自服务的任何指令。

微型端口驱动程序将其 MB 设备的初始就绪状态设置为**WwanReadyStateOff**。 当他们继续初始化时，微型端口驱动程序必须发送事件通知，以通知 MB 服务对其设备就绪状态的更改。

如果小型端口驱动程序遇到任何错误条件，则必须停止该初始化过程。 清除错误条件后，微型端口驱动程序可以恢复初始化过程，直到其设备达到**WwanReadyStateInitialized**就绪状态。

下面是一些错误情况的示例：

-   如果设备要求使用 SIM 卡，而微型端口驱动程序检测到不存在 SIM 卡，则微型端口驱动程序必须发送**WwanReadyStateSimNotInserted**就绪状态事件通知，并且微型端口驱动程序必须保持该状态，直到用户将 SIM 卡插入设备。

-   如果设备要求使用 SIM 卡，而微型端口驱动程序无法读取已插入的 SIM 卡（例如，插入到基于 GSM 的设备中的 U 形，或插入到基于 CDMA 的设备中的 USIM）或 SIM 卡与设备不兼容（例如， 3G USIM 插入到2G 设备中，该设备无法解释 USIM 格式），微型端口驱动程序必须发送**WwanReadyStateBadSim** ready 事件通知，并且在用户插入正确的 SIM 卡之前，微型端口驱动程序必须保持该状态到设备中。

-   如果设备被 PIN 锁定（对于使用 SIM 卡的设备）或通过密码（对于不使用 SIM 卡的设备）来阻止进一步的设备初始化进度，则微型端口驱动程序必须发送**WwanReadyStateDeviceLocked**就绪状态事件通知和微型端口驱动程序必须保持该状态，直到用户输入正确的 PIN 或密码。

-   如果微型端口驱动程序检测到需要进行服务激活，则微型端口驱动程序必须发送**WwanReadyStateNotActivated**就绪状态事件通知，并且必须保持该状态，直到服务已激活。 这是北美中基于 CDMA 的设备的典型行为。

-   如果微型端口驱动程序运行的不是前面提到的故障，微型端口驱动程序必须发送**WwanReadyStateFailure**的就绪状态事件通知，并且必须保持该状态，直至确定问题并更正.

请注意，MB 服务不假定微型端口驱动程序可以检测所有这些错误。 服务也不会假设小型小型驱动程序检测这些错误情况的顺序。 不过，最好按照前面列出的顺序来实现错误方案。

在微型端口驱动程序发送**WwanReadyStateInitialized**的就绪状态事件通知之前，该服务将不会继续进行与网络相关的活动，直到发现并更正该问题。 但是，该服务仍可以将 Oid 发送到微型端口驱动程序。

在报告**WwanReadyStateInitialized**就绪状态之前，微型端口驱动程序无需等待 SMS 子系统准备就绪。 相反，小型端口驱动程序应在 SMS 子系统准备发送和接收 SMS 消息时，将一个单独的[OID\_WWAN\_SMS\_配置](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-sms-configuration)通知。

### <a name="emergency-mode-support"></a>紧急模式支持

如果微型端口驱动程序指示它在处理[OID\_WWAN\_就绪\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)时支持紧急呼叫服务，则微型端口驱动程序必须设置[**WWAN\_就绪\_信息的 EmergencyMode 成员**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wwan/ns-wwan-_wwan_ready_info) **WwanEmergencyModeOn**的结构。 在这种情况下，微型端口驱动程序应继续将注册通知发送到 MB 服务，但该服务不会调用任何自动配置相关的功能。

微型端口驱动程序可以指定它们支持紧急呼叫服务，即使在检测到 SIM 失效的情况下也是如此，原因可能是订阅未付款，或服务已被停用，因为设备已被报告为被盗。

有关设备准备情况的详细信息，请参阅[OID\_WWAN\_就绪\_信息](https://docs.microsoft.com/windows-hardware/drivers/network/oid-wwan-ready-info)。

 

 





