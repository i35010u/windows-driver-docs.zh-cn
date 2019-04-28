---
title: 手机网络 COM API 功能
description: 本主题提供在移动电话的 COM API 功能的信息。
ms.assetid: f6172f25-9003-4b98-a87d-26dc193d40e3
keywords:
- COM API 功能，移动电话网络驱动程序
ms.date: 11/07/2017
ms.localizationpriority: medium
ms.openlocfilehash: e87107e64fd6fffd5c62e6f6e8cc4dc9bdbed98c
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341901"
---
# <a name="cellular-com-api-capabilities"></a>手机网络 COM API 功能

> [!WARNING]
> 移动电话的 COM API 在 Windows 10 中已弃用。 提供此内容是为了支持 OEM 和移动运营商创建的 Windows Phone 8.1 应用程序的维护。

若要允许移动电话网络 Api 来执行，功能必须添加到包文件包含移动电话应用程序。 对于每个应用程序调用的方法，包括所需的功能。

所有移动电话的 COM 接口方法都需要 ID_CAP_CELL_API_COMMON 功能。 增加了功能要求如下所示：

| 方法 | 除了 ID_CAP_CELL_API_COMMON 功能 |
| --- | --- |
| IOemCellularModem::SendModemOpaqueCommand | ID_CAP_CELL_API_OEM_PASSTHROUGH | 
| IOemCellularModem::RegisterForOpaqueModemNotifications | ID_CAP_CELL_API_OEM_PASSTHROUGH |
| IOemCellularModem::UnRegisterForOpaqueModemNotifications | ID_CAP_CELL_API_OEM_PASSTHROUGH |
| IOemCellularModem::SetRFState | ID_CAP_CELL_API_OEM_PASSTHROUGH | 
| IOemCellularModem::GetRFState | ID_CAP_CELL_API_OEM_PASSTHROUGH |
| IOemCan::GetPositionInfo | ID_CAP_CELL_API_LOCATION |
| IOemUiccApp::GetAppId | ID_CAP_CELL_API_UICC |
| IOemUiccApp::GetType | ID_CAP_CELL_API_UICC |
| IOemUiccApp::GetPinLockState | ID_CAP_CELL_API_UICC |
| IOemUiccApp::ReadRecord | ID_CAP_CELL_API_UICC, ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::WriteRecord | ID_CAP_CELL_API_UICC, ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::GetRecordStatusOnFilePath | ID_CAP_CELL_API_UICC |
| IOemUiccApp::ReadRecordOnFilePath | ID_CAP_CELL_API_UICC, ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::WriteRecordOnFilePath | ID_CAP_CELL_API_UICC, ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::GetIMSI | ID_CAP_CELL_API_UICC |
| IOemUiccApp::GetSIDNID | ID_CAP_CELL_API_UICC, ID_CAP_CELL_API_UICC_LOWLEVEL |
| IOemUiccApp::GetSubscriberNumbers | ID_CAP_CELL_API_UICC |
| IOemUiccAppEx2::GetNAI | ID_CAP_CELL_API_UICC |

## <a name="related-topics"></a>相关主题

[移动电话的 COM API 设计指南](cellular-com-api-design-guide.md)

[移动电话的 COM API 参考](https://msdn.microsoft.com/library/windows/hardware/dn946508)

