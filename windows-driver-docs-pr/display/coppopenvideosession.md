---
title: COPPOpenVideoSession 函数
description: 示例 COPPOpenVideoSession 函数初始化用于当前视频会话的 COPP DirectX VA 设备对象。
keywords:
- 复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，视频微型端口驱动程序代码模板
- 视频微型端口驱动程序 WDK Windows 2000，COPP 代码模板
- 认证的输出保护协议
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2542782b95e16f19a67b6f5fd6d17246b9e346bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791809"
---
# <a name="coppopenvideosession-function"></a>COPPOpenVideoSession 函数

示例 COPPOpenVideoSession 函数初始化用于当前视频会话的 COPP DirectX VA 设备对象。

### <a name="syntax"></a>语法

```cpp
HRESULT COPPOpenVideoSession(
  _In_ COPP_DeviceData pThis,
  _In_ ULONG           DevID
);
```

## <a name="parameters"></a>参数

*pThis [in]*

* 指向 COPP DirectX VA 设备对象的指针。

*DevID [in]*

* 提供 COPP 设备附加到的图形设备的标识符。

## <a name="return-value"></a>返回值

如果成功，则返回零 (S_OK 或 DD_OK) ;否则，将返回错误代码。

## <a name="remarks"></a>备注

在调用 COPP 设备类的任何其他成员函数之前，必须通过对 COPPOpenVideoSession 的调用对 COPP 设备进行初始化。 COPPOpenVideoSession 应将 (设置为 0) 视频会话的每个受支持保护类型的本地保护级别，并递增相应的全局保护级别计数器。 有关详细信息，请参阅处理保护级别。

如果由 DevID 参数标识的设备驱动多个使用双屏以外模式的图形适配器，COPPOpenVideoSession 应返回 DDERR_UNSUPPORTEDMODE。 有关详细信息，请参阅 COPP 和 Multiple-Monitor 支持。

示例 COPPOpenVideoSession 函数直接映射到 DD_MOTIONCOMPCALLBACKS 结构的 CreateMoComp 成员。 CreateMoComp 成员指向显示驱动程序提供的 DdMoCompCreate 回调函数，该函数引用 DD_CREATEMOCOMPDATA 结构。 DD_CREATEMOCOMPDATA 的 lpGuid 成员指向 COPP DirectX VA 设备 GUID。

## <a name="example-code"></a>示例代码

下面的代码提供了一个示例，说明如何实现 COPPOpenVideoSession 函数：

```cpp
HRESULT
COPPOpenVideoSession(
    COPP_DeviceData* pThis,
    DWORD DevID
    )
{
    DWORD i;
    pThis->m_DevID = DevID;
    pThis->m_CmdSeqNumber = (DWORD)-1;
    pThis->m_StatusSeqNumber = (DWORD)-1;
    pThis->m_COPPDevState = COPP_OPENED;
    memset(&pThis->m_AesHelper, 0, sizeof(pThis->m_AesHelper));
    //
    // make sure the session protection levels are reset
    //
    memset(&pThis->m_LocalLevel, 0, sizeof(pThis->m_LocalLevel));
    //
    // initialize the session local protection levels and
    // increment the corresponding global protection level counter
    //
    // enumerate all the protection types supported by this connector
    DWORD j;
    for (j = COPP_ProtectionType_HDCP, i = COPP_ProtectionTypeIndex_HDCP;
         j & COPP_ProtectionType_Mask; j <<= 1, i++) {
        // for each type supported, make sure the initial level
        // is set correctly
        if (g_ConnectorInfo[pThis->m_DevID].ProtectionTypeMask & j) {
            pThis->m_LocalLevel[i] = 0;
            g_COPPLevels[pThis->m_DevID].Levels[i][0]++;
        }
        else {
            pThis->m_LocalLevel[i] = COPP_NoProtectionLevelAvailable;
        }
    }
    return NO_ERROR;
}
```

**惠?**

| 目标平台 | 版本 |
| -- | -- |
| 台式机 | 此函数仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。 |
