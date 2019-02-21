---
title: COPP 设备定义模板代码
description: COPP 设备定义模板代码
ms.assetid: 86cafb33-f92a-4c5d-8a54-37aab5e79f37
keywords:
- COPP 设备 WDK DirectX VA
- 复制保护 WDK COPP，COPP 设备
- COPP WDK DirectX VA，COPP 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d3910502765c9a12daed1639d4c70b71de4b9424
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526479"
---
# <a name="copp-device-definition-template-code"></a>COPP 设备定义模板代码


## <span id="ddk_copp_device_definition_template_code_gg"></span><span id="DDK_COPP_DEVICE_DEFINITION_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 和更高版本，和 Windows XP SP2 及更高版本。

使用下面的示例代码来定义 COPP DirectX VA 设备对象。

```cpp
#define COPP_OPENED                 0
#define COPP_CERT_LENGTH_RETURNED   1
#define COPP_KEY_EXCHANGED          2
#define COPP_SESSION_ACTIVE         3
typedef struct {
    DWORD   m_LocalLevel[COPP_MAX_TYPES];
    GUID    m_KDI;
    DWORD   m_CmdSeqNumber;
    DWORD   m_StatusSeqNumber;
    DWORD   m_rGraphicsDriver;
    DWORD   m_COPPDevState;
    DWORD   m_DevID;

    AESHelper   m_AesHelper;

} COPP_DeviceData;
```

 

 





