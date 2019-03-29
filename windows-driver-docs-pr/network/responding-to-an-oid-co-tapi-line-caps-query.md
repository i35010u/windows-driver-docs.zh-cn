---
title: 响应 OID_CO_TAPI_LINE_CAPS 查询
description: 响应 OID_CO_TAPI_LINE_CAPS 查询
ms.assetid: b1ca65c6-ecce-4d2c-b7ca-03b6a334f97b
keywords:
- 语音流 WDK 网络、 支持规范
- OID_CO_TAPI_LINE_CAPS
- ulMediaModes
- ulAddressTypes
- UlGenerateDigitModes
- UlMonitorDigitModes
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 026f3cdc988bd6fdcbb7ea1e5ae71eecca36bcd4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568563"
---
# <a name="responding-to-an-oidcotapilinecaps-query"></a>响应的 OID\_CO\_TAPI\_行\_CAPS 查询





以响应[OID\_共同\_TAPI\_行\_CAPS](https://msdn.microsoft.com/library/windows/hardware/ff569098)查询、 呼叫管理器或 MCM 返回共同\_TAPI\_行\_CAPS 结构包含一条线\_开发人员\_CAPS 结构。 若要支持语音流式处理，呼叫管理器或 MCM 必须指定以下值的行中\_开发人员\_CAPS 结构：

-   **ulMediaModes**

    此字段应包含 LINEMEDIAMODE\_AUTOMATEDVOICE，映射到 TAPIMEDIAMODE\_音频 TAPI 3.0 中。

-   **ulAddressTypes**

    必须相应地填充此字段。 有关有效值的说明，请参阅的说明**dwAddressTypes** Microsoft Windows SDK 文档中。 此字段不能为零。

-   **ulGenerateDigitModes**

    此字段必须填充 LINEDIGITMODE 的按位 OR\_在行指定可以生成的数字模式的常量。 说明 LINEDIGITMODE\_常量，请参阅的说明**dwGenerateDigitModes** Windows SDK 文档中。

-   **ulMonitorDigitModes**

    此字段必须填充 LINEDIGITMODE 的按位 OR\_行中指定的位模式不是可以检测到此常量。 有关说明 LINEDIGITMODE\_常量，请参阅的说明**dwMonitorDigitModes** Windows SDK 文档中。

 

 





