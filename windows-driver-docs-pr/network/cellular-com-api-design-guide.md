---
title: 移动电话的 COM API 设计指南
description: 本部分提供在移动电话的 COM API 的信息。
ms.assetid: 93aa20d0-d8c3-40ec-baf1-fab56ff5686d
keywords:
- 移动电话 COM API 设计指南网络驱动程序
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8da7aa11d0d6e2b5d35a87d593cdd8aa3ba965f3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522659"
---
# <a name="cellular-com-api-design-guide"></a>移动电话的 COM API 设计指南

> [!WARNING]
> 移动电话的 COM API 在 Windows 10 中已弃用。 提供此内容是为了支持 OEM 和移动运营商创建的 Windows Phone 8.1 应用程序的维护。

本部分提供在移动电话的 COM API 的信息。

由两个 Microsoft 接口定义语言 (MIDL) 文件提供的接口：

- cellularapi_oem.idl
- rilapitypes.idl

使用 MIDL 编译器生成标头文件。 有关详细信息，请参阅[Microsoft 接口定义语言](https://msdn.microsoft.com/library/windows/desktop/aa367091)Windows 开发人员中心上。

必须声明相应功能中包含的移动电话应用程序的包。 有关详细信息，请参阅[移动电话的 COM API 功能](cellular-com-api-capabilities.md)。

## <a name="in-this-section"></a>本部分内容

[移动电话的 COM API 功能](cellular-com-api-capabilities.md)

[使用 IOemCellularModem 接口与 RIL 驱动程序进行通信](communicate-with-the-ril-driver-by-using-the-ioemcellularmodem-interface.md)

## <a name="related-topics"></a>相关主题

[移动电话的 COM API 参考](https://msdn.microsoft.com/library/windows/hardware/dn946508)

