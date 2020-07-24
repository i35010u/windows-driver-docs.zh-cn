---
title: COPPQueryStatus 函数
description: 示例 COPPQueryStatus 函数检索与 COPP DirectX VA 设备关联的受保护视频会话的状态。
ms.assetid: c2265df7-8b60-4a14-b7dc-ee227ad062dc
keywords:
- 复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，视频微型端口驱动程序代码模板
- 视频微型端口驱动程序 WDK Windows 2000，COPP 代码模板
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef7ba2580ec60903c9398d4112493bb60ea3d6e1
ms.sourcegitcommit: df50dc10210c124f2c7fb173d6e4fb796f56e5bd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/22/2020
ms.locfileid: "86949722"
---
# <a name="coppquerystatus-function"></a>COPPQueryStatus 函数

示例 COPPQueryStatus 函数检索与 COPP DirectX VA 设备关联的受保护视频会话的状态。

### <a name="syntax"></a>语法

```cpp
HRESULT COPPQueryStatus(
  _In_  COPP_DeviceData       pThis,
  _In_  DXVA_COPPStatusInput  *pInput,
  _Out_ DXVA_COPPStatusOutput *pOutput
);
```

## <a name="parameters"></a>参数

*pThis [in]*

* 指向 COPP DirectX VA 设备对象的指针。

*pInput [in]*

* 提供一个指向 DXVA_COPPStatusInput 结构的指针，该结构包含检索特定状态信息的请求。

*pOutput [out]*

* 指向 DXVA_COPPStatusOutput 结构的指针，该结构接收有关所使用的物理连接器的状态信息。

## <a name="return-value"></a>返回值

如果成功，则返回零（S_OK 或 DD_OK）;否则，将返回错误代码。

## <a name="remarks"></a>备注

在关联的 COPP DirectX VA 设备收到对其 COPPQueryStatus 函数的调用之前，视频会话应设置为 "保护模式" （即，它应为 "活动"）。 也就是说，应在 COPPQueryStatus 之前调用 COPPSequenceStart 函数。 如果在 COPPSequenceStart 之前调用 COPPQueryStatus，则 COPPQueryStatus 应返回 E_UNEXPECTED。

COPPQueryStatus 函数接收包含状态请求的 pInput 中填充的 DXVA_COPPStatusInput 结构。 COPPQueryStatus 函数处理请求，并在 pOutput 的 DXVA_COPPStatusOutput 结构中返回相应的状态。

## <a name="mapping-rendermocomp-to-coppquerystatus"></a>将 RenderMoComp 映射到 COPPQueryStatus

示例 COPPQueryStatus 函数直接映射到对 DD_MOTIONCOMPCALLBACKS 结构的 RenderMoComp 成员的调用。 RenderMoComp 成员指向显示驱动程序提供的 DdMoCompRender 回调函数，该函数引用 DD_RENDERMOCOMPDATA 结构。

调用 RenderMoComp 回调函数时，不会首先调用显示驱动程序提供的 BeginMoCompFrame 或 EndMoCompFrame 函数。

按如下所示填充 DD_RENDERMOCOMPDATA 结构。

| 成员 | 值 |
| ------ | ----- |
| dwNumBuffers | Zero。 |
| lpBufferInfo | NULL。 |
| dwFunction | DXVA_COPPQueryStatusFnCode 常量（在 DXVA 中定义）。 |
| lpInputData | 指向 DXVA_COPPStatusInput 结构的指针。 |
| lpOutputData | 指向 DXVA_COPPStatusOutput 结构的指针。 |

## <a name="example-code"></a>示例代码

下面的代码提供了一个示例，说明如何实现 COPPQueryStatus 函数：

```cpp
HRESULT
COPPQueryStatus(
    COPP_DeviceData* pThis,
    DXVA_COPPStatusInput* pStatusInput,
    DXVA_COPPStatusOutput* pStatusOutput
    )
{
    if (pThis->m_COPPDevState != COPP_SESSION_ACTIVE) {
        return E_UNEXPECTED;
    }
    if (pStatusInput->dwSequence != pThis->m_StatusSeqNumber) {
        return E_INVALIDARG;
    }
    //
    // reset the output buffer
    //
    memset(pStatusOutput, 0, sizeof(DXVA_COPPStatusOutput));
    if (IsEqualGUID(&DXVA_COPPQueryConnectorType, &pStatusInput->guidStatusRequestID)) {
        // Verify no input data for this status request.
        if (pStatusInput->cbSizeData != 0) {
            return E_INVALIDARG;
        }
        DXVA_COPPStatusData Tmp;
        Tmp.rApp = pStatusInput->rApp;
        Tmp.dwData = g_ConnectorInfo[pThis->m_DevID].ConnType;
        Tmp.dwFlags = COPP_StatusNormal;
        pStatusOutput->cbSizeData = sizeof(Tmp);
        memcpy(pStatusOutput->COPPStatus, &Tmp,sizeof(Tmp));
    }
    else if (IsEqualGUID(&DXVA_COPPQueryProtectionType, &pStatusInput->guidStatusRequestID)) {
        // verify that there is no input data for this status request
        if (pStatusInput->cbSizeData != 0) {
            return E_INVALIDARG;
        }
        DXVA_COPPStatusData Tmp;
        Tmp.rApp = pStatusInput->rApp;
        Tmp.dwData = g_ConnectorInfo[pThis->m_DevID].ProtectionTypeMask;
        Tmp.dwFlags = COPP_StatusNormal;
        pStatusOutput->cbSizeData = sizeof(Tmp);
        memcpy(pStatusOutput->COPPStatus, &Tmp,sizeof(Tmp));
    }
    else if (IsEqualGUID(&DXVA_COPPQueryLocalProtectionLevel, &pStatusInput->guidStatusRequestID) ||
             IsEqualGUID(&DXVA_COPPQueryGlobalProtectionLevel, &pStatusInput->guidStatusRequestID)) {
        DWORD ProtType;
        DWORD ProtIndex;
        DWORD Level;
        // verify that there is a single DWORD input data for this status request
        if (pStatusInput->cbSizeData != sizeof (DWORD)) {
            return E_INVALIDARG;
        }
        memcpy(&ProtType, (LPVOID)&pStatusInput->StatusData[0], sizeof(DWORD));
        // verify that no invalid protection type bits are set
        if (ProtType & ~COPP_ProtectionType_Mask) {
            return E_INVALIDARG;
        }
        // verify that only the protection level of a single protection type is requested
        ProtIndex = MapProtectionTypeToProtectionIndex(ProtType);
        if (ProtIndex == COPP_ProtectionTypeIndex_Unkonwn) {
            return E_INVALIDARG;
        }
        // verify that the video session supports the protection type
        if (!(g_ConnectorInfo[pThis->m_DevID].ProtectionTypeMask & ProtType)) {
            return E_INVALIDARG;
        }
        if (IsEqualGUID(&DXVA_COPPQueryLocalProtectionLevel,
                        &pStatusInput->guidStatusRequestID)) {
            Level = pThis->m_LocalLevel[ProtIndex];
        }
        else {
            Level = g_nLevels[ProtIndex] - 1;
            for ( ; Level != 0; Level--) {
                if (g_COPPLevels[pThis->m_DevID].Levels[ProtIndex][Level]) {
                    break;
                }
            }
        }
        DXVA_COPPStatusData Tmp;
        Tmp.rApp = pStatusInput->rApp;
        Tmp.dwData = Level;
        Tmp.dwFlags = COPP_StatusNormal;
        pStatusOutput->cbSizeData = sizeof(Tmp);
        memcpy(pStatusOutput->COPPStatus, &Tmp, sizeof(Tmp));
    }
    pThis->m_StatusSeqNumber++;
    pStatusOutput->macKDI = COPP_CalculateMAC(&pThis->m_AesHelper,
                                    (BYTE*)&pStatusOutput->cbSizeData,
                         sizeof(DXVA_COPPStatusOutput) - sizeof(GUID),
                                     &pThis->m_KDI);
    return NO_ERROR;
}
```

**惠?**

| 目标平台 | 版本 |
| -- | -- |
| “桌面” | 此函数仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。 |
