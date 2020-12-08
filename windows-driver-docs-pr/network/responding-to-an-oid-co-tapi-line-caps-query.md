---
title: 响应 OID_CO_TAPI_LINE_CAPS 查询
description: 响应 OID_CO_TAPI_LINE_CAPS 查询
keywords:
- 语音流 WDK 网络，支持规范
- OID_CO_TAPI_LINE_CAPS
- ulMediaModes
- ulAddressTypes
- UlGenerateDigitModes
- UlMonitorDigitModes
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 99cf7b79ad47fbbc3be7172278c51efea2868108
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817079"
---
# <a name="responding-to-an-oid_co_tapi_line_caps-query"></a>响应 OID \_ CO \_ TAPI \_ LINE \_ cap 查询





为了响应 [OID \_ CO \_ TAPI \_ 线路 \_ cap](./oid-co-tapi-line-caps.md) 查询，呼叫管理器或 MCM 返回一个 \_ \_ \_ 包含行 \_ DEV cap 结构的 CO TAPI 线帽结构 \_ 。 若要支持语音流，呼叫管理器或 MCM 必须在 "开发者 cap" 行中指定以下值 \_ \_ ：

-   **ulMediaModes**

    此字段应包含 \_ 映射到 TAPI 3.0 TAPIMEDIAMODE 音频的 LINEMEDIAMODE AUTOMATEDVOICE \_ 。

-   **ulAddressTypes**

    必须正确填写此字段。 有关有效值的说明，请参阅 Microsoft Windows SDK 文档中的 **dwAddressTypes** 说明。 此字段不能为零。

-   **ulGenerateDigitModes**

    必须使用 LINEDIGITMODE 常量的按位 "或" 填充此字段 \_ ，这些常量指定可在行上生成的数字模式。 有关 LINEDIGITMODE 常量的说明 \_ ，请参阅 Windows SDK 文档中的 **dwGenerateDigitModes** 的说明。

-   **ulMonitorDigitModes**

    必须使用 LINEDIGITMODE 常量的按位 "或" 填充此字段 \_ ，这些常量指定的数字模式可以在此行上检测到。 有关 LINEDIGITMODE 常量的说明 \_ ，请参阅 Windows SDK 文档中的 **dwMonitorDigitModes** 说明。

 

