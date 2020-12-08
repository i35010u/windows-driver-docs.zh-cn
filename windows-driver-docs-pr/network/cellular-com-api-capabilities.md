---
title: 手机网络 COM API 功能
description: 本主题提供有关蜂窝 COM API 功能的信息。
keywords:
- 移动电话 COM API 功能网络驱动程序
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a84c8e9808b525549a6d78d67943b9905898bad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826977"
---
# <a name="cellular-com-api-capabilities"></a>手机网络 COM API 功能

> [!WARNING]
> Windows 10 中已弃用蜂窝 COM API。 提供此内容是为了支持维护 Windows Phone 8.1 应用程序创建的 OEM 和移动运营商。

若要允许执行蜂窝 Api，必须将功能添加到包含移动电话应用程序的包文件。 对于应用程序调用的每个方法，都包含所需的功能。

所有蜂窝 COM 接口方法都需要 ID_CAP_CELL_API_COMMON 功能。 其他功能要求如下所示：

| 方法 | 除 ID_CAP_CELL_API_COMMON 以外的功能 |
| --- | --- |
| IOemCellularModem::SendModemOpaqueCommand | ID_CAP_CELL_API_OEM_PASSTHROUGH | 
| IOemCellularModem::RegisterForOpaqueModemNotifications | ID_CAP_CELL_API_OEM_PASSTHROUGH |
| IOemCellularModem::UnRegisterForOpaqueModemNotifications | ID_CAP_CELL_API_OEM_PASSTHROUGH |
| IOemCellularModem::SetRFState | ID_CAP_CELL_API_OEM_PASSTHROUGH | 
| IOemCellularModem::GetRFState | ID_CAP_CELL_API_OEM_PASSTHROUGH |
| IOemCan::GetPositionInfo | ID_CAP_CELL_API_LOCATION |
| IOemUiccApp::GetAppId | ID_CAP_CELL_API_UICC |
| IOemUiccApp：： GetType | ID_CAP_CELL_API_UICC |
| IOemUiccApp::GetPinLockState | ID_CAP_CELL_API_UICC |
| IOemUiccApp::ReadRecord | ID_CAP_CELL_API_UICC，ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::WriteRecord | ID_CAP_CELL_API_UICC，ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::GetRecordStatusOnFilePath | ID_CAP_CELL_API_UICC |
| IOemUiccApp::ReadRecordOnFilePath | ID_CAP_CELL_API_UICC，ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::WriteRecordOnFilePath | ID_CAP_CELL_API_UICC，ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::GetIMSI | ID_CAP_CELL_API_UICC |
| IOemUiccApp::GetSIDNID | ID_CAP_CELL_API_UICC，ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::GetSubscriberNumbers | ID_CAP_CELL_API_UICC |
| IOemUiccAppEx2::GetNAI | ID_CAP_CELL_API_UICC |

## <a name="related-topics"></a>相关主题

[手机网络 COM API 设计指南](cellular-com-api-design-guide.md)

[蜂窝 COM API 参考](/previous-versions/windows/hardware/cellular/dn946508(v=vs.85))
