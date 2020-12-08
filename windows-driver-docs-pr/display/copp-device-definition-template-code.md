---
title: COPP 设备定义模板代码
description: COPP 设备定义模板代码
keywords:
- COPP 设备 WDK DirectX VA
- 复制保护 WDK COPP，COPP 设备
- COPP WDK DirectX VA，COPP 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd4460682efc3d60fcfe3334e55b70b21376b23a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824227"
---
# <a name="copp-device-definition-template-code"></a>COPP 设备定义模板代码


## <span id="ddk_copp_device_definition_template_code_gg"></span><span id="DDK_COPP_DEVICE_DEFINITION_TEMPLATE_CODE_GG"></span>


本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。

使用以下示例代码定义 COPP DirectX VA 设备对象。

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

 

 





