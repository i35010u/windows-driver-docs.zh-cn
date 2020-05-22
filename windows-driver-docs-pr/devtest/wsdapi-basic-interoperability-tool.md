---
title: WSDAPI 基本互操作性工具
description: WSDAPI 基本互操作性工具
ms.assetid: c4a610d4-3adf-406d-88d6-0879eb98b54f
keywords:
- 工具 WDK，测试驱动程序
- WSDBIT 工具 WDK
- WSDAPI 基本互操作性工具 WDK
- DWPS WDK
- Web 服务 WDK 的设备配置文件
- 用于设备的 Web 服务 API WDK
- WSDAPI WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfe9df72d7ef2dbc2aa2241c5704eafec32c2371
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769507"
---
# <a name="wsdapi-basic-interoperability-tool"></a>WSDAPI 基本互操作性工具


[Web services 的设备配置文件（DPWS）](http://schemas.xmlsoap.org/ws/2005/05/devprof/)是一种引用规范，可汇编和约束若干 Web 服务（WS）规范。 [Web 服务设备（WSD）](https://docs.microsoft.com/windows/win32/wsdapi/wsd-portal) API （WSDAPI）是 Windows 附带的 DPWS 实现。 Windows 使用 WSDAPI 来发现任何类型的 DPWS 设备，并使用 WSDAPI 将控制消息发布到多个设备类，如打印机、扫描仪和网络投影仪。

WSDAPI 基本互操作性工具（WSDBIT）可用于验证 Windows 是否可以与非 WSDAPI DPWS 堆栈进行互操作。 此工具主要用于实现 DPWS 的设备开发人员以及要测试与 Windows 的互操作性。 某些 WSDBIT 测试要求设备实现一个特殊的测试接口，该接口用于运用高级 DPWS 功能，如[SOAP 消息传输优化机制（MTOM）](https://www.w3.org/TR/2005/REC-soap12-mtom-20050125/) （用于消息附件）和[Web 服务事件](https://docs.microsoft.com/previous-versions/ms951233(v=msdn.10))。 这些接口并不是绝对必需的。 但是，它们是在 WSDBIT 中涵盖此功能的唯一方法。

WSDAPI 实现了规范的客户端和设备部分，而 WSDBIT 可用于将 WSDAPI 作为客户端或设备使用。 WSDBIT 可用于测试和验证非 WSDAPI 设备或非 WSDAPI 客户端。

阅读关于 WSD 互操作性工具之前，应熟悉 DPWS 规范及其[引用的规范](referenced-namespaces.md)。

**注意**   WSDBIT 可用于帮助实现设备上的 DPWS，但并不是一种通用的调试工具。 其他[wsdapi 开发工具](https://docs.microsoft.com/windows/win32/wsdapi/wsdapi-development-tools)（如[WSDAPI 调试工具](https://docs.microsoft.com/windows/win32/wsdapi/debugging-tools)）更适合用于观察流量和诊断故障。 这些工具适用于桌面应用的 Windows SDK，请参阅[用于开发桌面应用的下载](https://developer.microsoft.com/windows/downloads/windows-10-sdk/)。

 

本节包括下列主题：

[WSDBIT 简介](introduction-to-wsdbit.md)

[参考的命名空间](referenced-namespaces.md)

[WSDBIT 测试环境](wsdbit-testing-environment.md)

[WSDBIT 的客户端方案](client-scenarios-for-wsdbit.md)

[WSDBIT 参考](wsdbit-reference.md)

有关 WSD 和 WSDAPI 的详细信息，请参阅 Windows 软件开发工具包（SDK）中的以下主题：

-   [WSD 设备开发](https://docs.microsoft.com/windows/win32/wsdapi/wsd-device-development)

-   [Windows 上的 WSD 应用程序开发](https://docs.microsoft.com/windows/win32/wsdapi/wsd-application-development-on-windows)

-   [WSDAPI 故障排除指南](https://docs.microsoft.com/windows/win32/wsdapi/wsdapi-troubleshooting-guide)

 

 





