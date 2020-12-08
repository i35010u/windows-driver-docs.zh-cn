---
title: COPPCloseVideoSession 函数
description: 示例 COPPCloseVideoSession 函数关闭用于当前视频会话的 COPP DirectX VA 设备对象。
keywords:
- 复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，视频微型端口驱动程序代码模板
- 视频微型端口驱动程序 WDK Windows 2000，COPP 代码模板
- 认证的输出保护协议
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 35523b75d29fdd605ebb4c3264f0aa32b469ce9d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787555"
---
# <a name="coppclosevideosession-function"></a>COPPCloseVideoSession 函数

示例 COPPCloseVideoSession 函数关闭用于当前视频会话的 COPP DirectX VA 设备对象。

### <a name="syntax"></a>语法

```cpp
HRESULT COPPCloseVideoSession(
  _In_ COPP_DeviceData pThis
);
```

## <a name="parameters"></a>参数

*pThis [in]*

* 指向 COPP DirectX VA 设备对象的指针。

## <a name="return-value"></a>返回值

如果成功，则返回零 (S_OK 或 DD_OK) ;否则，将返回错误代码。

## <a name="remarks"></a>备注

当视频会话仍在应用输出保护时，可以调用 COPPCloseVideoSession 函数。 COPPCloseVideoSession 应撤消 COPP DirectX VA 设备对象的保护设置，并相应地调整全局保护设置。

COPPCloseVideoSession 函数直接映射到 DD_MOTIONCOMPCALLBACKS 结构的 DestroyMoComp 成员。 DestroyMoComp 成员指向显示器驱动程序提供的 DdMoCompDestroy 回调函数。

## <a name="example-code"></a>示例代码

下面的代码提供了一个示例，说明如何实现 COPPCloseVideoSession 函数：

```cpp
HRESULT
COPPCloseVideoSession(
    COPP_DeviceData* pThis
    )
{
    DWORD j, i;
    // enumerate all the protection types supported by this connector
    for (j = COPP_ProtectionType_HDCP, i = COPP_ProtectionTypeIndex_HDCP;
         j & COPP_ProtectionType_Mask; j <<= 1, i++) {
        // for each type supported, make sure the initial level
        // is set correctly
        if (g_ConnectorInfo[pThis->m_DevID].ProtectionTypeMask & j) {
            DWORD oldLevel = pThis->m_LocalLevel[i];
            g_COPPLevels[pThis->m_DevID].Levels[i][oldLevel]--;
        }
    }
    ResetKey(&pThis->m_AesHelper);
    return NO_ERROR;
}
```

**惠?**

| 目标平台 | 版本 |
| -- | -- |
| 台式机 | 此函数仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。 |
