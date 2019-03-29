---
title: COPPOpenVideoSession 函数
description: 示例 COPPOpenVideoSession 函数将初始化为当前的视频会话使用的 COPP DirectX VA 设备对象。
ms.assetid: 4fc318c8-c999-4623-91da-3a3fea83d7b4
keywords:
- 复制保护 WDK COPP，微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，微型端口驱动程序代码模板
- 微型端口驱动程序 WDK Windows 2000，COPP 代码模板
- 已认证的输出保护协议
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: ebf12e148b6df3cfbd273036dc0c308a41e35237
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564459"
---
# <a name="coppopenvideosession-function"></a>COPPOpenVideoSession 函数

示例 COPPOpenVideoSession 函数将初始化为当前的视频会话使用的 COPP DirectX VA 设备对象。

### <a name="syntax"></a>语法

```cpp
HRESULT COPPOpenVideoSession(
  _In_ COPP_DeviceData pThis,
  _In_ ULONG           DevID
);
```

## <a name="parameters"></a>Parameters

*pThis [in]*

* 指向 COPP DirectX VA 设备对象指针。

*[In] DevID*

* 提供 COPP 设备附加到图形设备的标识符。

## <a name="return-value"></a>返回值

返回零 （S_OK 或 DD_OK） 如果成功，则否则，返回错误代码。

## <a name="remarks"></a>备注

COPP 设备类的任何其他成员函数调用之前，必须通过调用 COPPOpenVideoSession 初始化 COPP 设备。 COPPOpenVideoSession 应初始化 （设置为 0） 的每个受支持的保护类型和相应的全局保护级别计数器递增视频会话的本地的保护级别。 有关详细信息，请参阅处理保护级别。

如果使用非双视图模式的多个图形适配器由 DevID 参数驱动器标识设备，COPPOpenVideoSession 应返回 DDERR_UNSUPPORTEDMODE。 有关详细信息，请参阅 COPP 和多监视器支持。

示例 COPPOpenVideoSession 函数直接映射到 DD_MOTIONCOMPCALLBACKS 结构的 CreateMoComp 成员。 CreateMoComp 成员指向显示驱动程序提供 DdMoCompCreate 回调的函数的引用 DD_CREATEMOCOMPDATA 结构。 DD_CREATEMOCOMPDATA lpGuid 成员指向 COPP DirectX VA 设备 GUID。

## <a name="example-code"></a>示例代码

以下代码举例说明如何实现 COPPOpenVideoSession 函数：

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

**要求**

| 目标平台 | 版本 |
| -- | -- |
| 桌面设备 | 此函数仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。 |
