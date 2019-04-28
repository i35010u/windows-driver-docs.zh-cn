---
title: COPPCloseVideoSession 函数
description: 示例 COPPCloseVideoSession 函数关闭当前的视频会话使用 COPP DirectX VA 设备对象。
ms.assetid: 27a6a23d-e9e8-403e-87b9-3ab0a07789cb
keywords:
- 复制保护 WDK COPP，微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，微型端口驱动程序代码模板
- 微型端口驱动程序 WDK Windows 2000，COPP 代码模板
- 已认证的输出保护协议
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1b7f834af8092318730cc21061694c29241b3755
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331313"
---
# <a name="coppclosevideosession-function"></a>COPPCloseVideoSession 函数

示例 COPPCloseVideoSession 函数关闭当前的视频会话使用 COPP DirectX VA 设备对象。

### <a name="syntax"></a>语法

```cpp
HRESULT COPPCloseVideoSession(
  _In_ COPP_DeviceData pThis
);
```

## <a name="parameters"></a>Parameters

*pThis [in]*

* 指向 COPP DirectX VA 设备对象指针。

## <a name="return-value"></a>返回值

返回零 （S_OK 或 DD_OK） 如果成功，则否则，返回错误代码。

## <a name="remarks"></a>备注

通过在视频会话仍应用输出保护时，可以调用 COPPCloseVideoSession 函数。 COPPCloseVideoSession 应撤消 COPP DirectX VA 设备对象的保护设置并调整全局保护设置相应地。

COPPCloseVideoSession 函数直接映射到 DD_MOTIONCOMPCALLBACKS 结构的 DestroyMoComp 成员。 DestroyMoComp 成员指向显示驱动程序提供 DdMoCompDestroy 回调函数。

## <a name="example-code"></a>示例代码

以下代码举例说明如何实现 COPPCloseVideoSession 函数：

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

**要求**

| 目标平台 | Version |
| -- | -- |
| 桌面设备 | 此函数仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。 |
