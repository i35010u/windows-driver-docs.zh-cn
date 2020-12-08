---
title: 手机网络 COM API 设计指南
description: 本部分提供有关蜂窝 COM API 的信息。
keywords:
- 移动电话 COM API 设计指南网络驱动程序
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7f73f7963bf0179cd57246df7e7ec6032269ec78
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787303"
---
# <a name="cellular-com-api-design-guide"></a>手机网络 COM API 设计指南

> [!WARNING]
> Windows 10 中已弃用蜂窝 COM API。 提供此内容是为了支持维护 Windows Phone 8.1 应用程序创建的 OEM 和移动运营商。

本部分提供有关蜂窝 COM API 的信息。

接口由两个 Microsoft 接口定义语言 (MIDL) 文件提供：

- cellularapi_oem .idl
- rilapitypes .idl

使用 MIDL 编译器生成标头文件。 有关详细信息，请参阅 Windows 开发人员中心上的 [Microsoft 接口定义语言](/windows/desktop/Midl/midl-start-page) 。

必须在包含移动应用程序的包中声明相应的功能。 有关详细信息，请参阅 [蜂窝 COM API 功能](cellular-com-api-capabilities.md)。

## <a name="in-this-section"></a>在本节中

[手机网络 COM API 功能](cellular-com-api-capabilities.md)

[使用 IOemCellularModem 接口与 RIL 驱动程序通信](communicate-with-the-ril-driver-by-using-the-ioemcellularmodem-interface.md)

## <a name="related-topics"></a>相关主题

[蜂窝 COM API 参考](/previous-versions/windows/hardware/cellular/dn946508(v=vs.85))
