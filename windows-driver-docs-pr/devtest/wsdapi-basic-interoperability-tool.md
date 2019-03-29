---
title: WSDAPI 基本互操作性工具
description: WSDAPI 基本互操作性工具
ms.assetid: c4a610d4-3adf-406d-88d6-0879eb98b54f
keywords:
- 工具 WDK，测试驱动程序
- WSDBIT 工具 WDK
- WSDAPI 基本互操作性工具 WDK
- DWPS WDK
- Web Services WDK 的的设备配置文件
- 设备 API WDK 的 web 服务
- WSDAPI WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db83d5879d5cc8b4c1d66ea078c67e3dcd5d8c35
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567300"
---
# <a name="wsdapi-basic-interoperability-tool"></a>WSDAPI 基本互操作性工具


[设备配置文件的 Web 服务 (DPWS)](https://go.microsoft.com/fwlink/p/?linkid=81255)是一种引用规范的汇编，并限制数 Web 服务 (WS) 规范。 [Web 服务上 Devices (WSD)](https://go.microsoft.com/fwlink/p/?linkid=163865) API (WSDAPI) 是 Windows 附带的 DPWS 的实现。 Windows 使用 WSDAPI 发现 DPWS 设备的任何类型，并且还使用 WSDAPI 将控制消息发送到多个设备类，如打印机、 扫描仪和网络投影仪。

WSDAPI 基本互操作性工具 (WSDBIT) 可以用于验证 Windows 可以与非 WSDAPI DPWS 堆栈互操作。 此工具主要面向设备开发人员要实现 DPWS，那些想要测试与 Windows 互操作性。 一些 WSDBIT 测试要求设备实现特殊的测试接口用来执行高级的 DPWS 功能，如[SOAP 消息传输优化机制 (MTOM)](https://go.microsoft.com/fwlink/p/?linkid=81254) （用于消息附件） 和[Web 服务事件](https://go.microsoft.com/fwlink/p/?linkid=81245)。 这些接口是不是绝对必需的。 但是，它们涵盖 WSDBIT 中的此功能的唯一方法。

WSDAPI 实现客户端和设备规范、 部分和 WSDBIT 可用于执行 WSDAPI 为客户端或设备。 WSDBIT 可以用于测试和验证非 WSDAPI 设备或非 WSDAPI 客户端。

阅读有关 WSD 互操作性工具之前，您应熟悉 DPWS 规范并将其[引用规范](referenced-namespaces.md)。

**请注意**  WSDBIT 可能用于帮助在设备上的 DPWS 实现但不是应为一个通用的调试工具。 其他[WSDAPI 开发工具](https://go.microsoft.com/fwlink/p/?linkid=163866)(如[WSDAPI 调试工具](https://go.microsoft.com/fwlink/p/?linkid=163867)) 更适合于观察流量和诊断故障。 适用于桌面应用程序的 Windows SDK 中提供了这些工具，请参阅[适用于开发桌面应用程序的下载]( https://go.microsoft.com/fwlink/p/?linkid=309790)。

 

本部分包括以下主题：

[WSDBIT 简介](introduction-to-wsdbit.md)

[引用的命名空间](referenced-namespaces.md)

[WSDBIT 测试环境](wsdbit-testing-environment.md)

[WSDBIT 的客户端方案](client-scenarios-for-wsdbit.md)

[WSDBIT 引用](wsdbit-reference.md)

有关 WSD 和 WSDAPI 的详细信息，请参阅 Windows 软件开发工具包 (SDK) 中的以下主题：

-   [WSD 设备开发](https://go.microsoft.com/fwlink/p/?linkid=163868)

-   [在 Windows 上的 WSD 应用程序开发](https://go.microsoft.com/fwlink/p/?linkid=163869)

-   [WSDAPI 故障排除指南](https://go.microsoft.com/fwlink/p/?linkid=163870)

 

 





