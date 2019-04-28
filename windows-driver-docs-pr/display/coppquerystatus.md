---
title: COPPQueryStatus 函数
description: 示例 COPPQueryStatus 函数检索与 COPP DirectX VA 设备相关联的受保护视频会话状态。
ms.assetid: c2265df7-8b60-4a14-b7dc-ee227ad062dc
keywords:
- 复制保护 WDK COPP，微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，微型端口驱动程序代码模板
- 微型端口驱动程序 WDK Windows 2000，COPP 代码模板
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab40601db1fdbeedf41b1dcc4c41e0fd2ffa6ad9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331351"
---
# <a name="coppquerystatus-function"></a>COPPQueryStatus 函数

示例 COPPQueryStatus 函数检索与 COPP DirectX VA 设备相关联的受保护视频会话状态。

### <a name="syntax"></a>语法

```cpp
HRESULT COPPQueryStatus(
  _In_  COPP_DeviceData       pThis,
  _In_  DXVA_COPPStatusInput  *pInput,
  _Out_ DXVA_COPPStatusOutput *pOutput
);
```

## <a name="parameters"></a>Parameters

*pThis [in]*

* 指向 COPP DirectX VA 设备对象指针。

*pInput [in]*

* 提供了指向包含要检索的特定状态信息的请求的 DXVA_COPPStatusInput 结构的指针。

*pOutput [out]*

* 指向接收有关正在使用的物理连接器的状态信息的 DXVA_COPPStatusOutput 结构的指针。

## <a name="return-value"></a>返回值

返回零 （S_OK 或 DD_OK） 如果成功，则否则，返回错误代码。

## <a name="remarks"></a>备注

视频会话应设置为受保护模式 （即，它应处于活动状态） 关联 COPP DirectX VA 之前设备接收到对其 COPPQueryStatus 函数的调用。 也就是说，COPPSequenceStart 函数应在 COPPQueryStatus 之前调用。 如果之前 COPPSequenceStart，将调用 COPPQueryStatus，COPPQueryStatus 应返回 E_UNEXPECTED。

COPPQueryStatus 函数接收包含状态请求的 pInput 填充的 DXVA_COPPStatusInput 结构。 COPPQueryStatus 函数处理该请求，并在 pOutput DXVA_COPPStatusOutput 结构中返回的相应状态。

## <a name="mapping-rendermocomp-to-coppquerystatus"></a>映射到 COPPQueryStatus RenderMoComp

示例 COPPQueryStatus 函数直接映射到 DD_MOTIONCOMPCALLBACKS 结构的 RenderMoComp 成员调用。 RenderMoComp 成员指向显示驱动程序提供 DdMoCompRender 回调的函数的引用 DD_RENDERMOCOMPDATA 结构。

而无需显示驱动程序提供 BeginMoCompFrame 或 EndMoCompFrame 要调用的函数首先调用 RenderMoComp 回调函数。

按如下所示填充 DD_RENDERMOCOMPDATA 结构。

|成员 |值 | |dwNumBuffers |为零。 | |lpBufferInfo |值为 NULL。 | |dwFunction |DXVA_COPPQueryStatusFnCode 常量 （dxva.h 中定义）。 | |lpInputData |指向 DXVA_COPPStatusInput 结构的指针。 | |lpOutputData |指向 DXVA_COPPStatusOutput 结构的指针。 |

## <a name="example-code"></a>示例代码

以下代码举例说明如何实现 COPPQueryStatus 函数：

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

**要求**

| 目标平台 | Version |
| -- | -- |
| 桌面设备 | 此函数仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。 |
