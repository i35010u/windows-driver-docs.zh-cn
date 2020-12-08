---
title: COPPCommand 函数
description: 示例 COPPCommand 函数在 COPP DirectX VA 设备上执行操作。
keywords:
- 复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，视频微型端口驱动程序代码模板
- 视频微型端口驱动程序 WDK Windows 2000，COPP 代码模板
- 认证的输出保护协议
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 69d207cf51a215b88135d46d48d0eefdd0aecfa1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787539"
---
# <a name="coppcommand-function"></a>COPPCommand 函数

示例 COPPCommand 函数在 COPP DirectX VA 设备上执行操作。

## <a name="syntax"></a>语法

```cpp
HRESULT COPPCommand(
  _In_ COPP_DeviceData  pThis,
  _In_ DXVA_COPPCommand *pCommand
);
```

## <a name="parameters"></a>参数

*pThis [in]*

 * 指向 COPP DirectX VA 设备对象的指针。

*pCommand [in]*
* 提供一个指向 DXVA_COPPCommand 结构的指针，该结构包含要在 COPP 设备上执行的操作的相关信息。

## <a name="return-value"></a>返回值

如果成功，则返回零 (S_OK 或 DD_OK) ;否则，将返回错误代码。

## <a name="remarks"></a>备注

视频会话应设置为 "保护模式" (即，在关联的 COPP DirectX VA 设备收到对其 COPPCommand 函数的调用之前，该会话应) 处于活动状态。 也就是说，应在 COPPCommand 之前调用 COPPSequenceStart 函数。 如果在 COPPSequenceStart 之前调用 COPPCommand，则 COPPCommand 应返回 E_UNEXPECTED。

COPPCommand 函数接收包含 COPP 命令的已填充 DXVA_COPPCommand 结构。 支持以下 COPP 命令：

* **DXVA_COPPSetProtectionLevel** <br>视频会话中的一条指令，用于设置与 COPP 设备关联的物理连接器的保护级别。 视频微型端口驱动程序应能够通过同一物理连接器支持多个视频会话。
* **DXVA_COPPSetSignaling** <br>说明如何保护通过与 DirectX VA COPP 设备关联的物理连接器的信号。

COPPCommand 函数应验证传递给它的参数对于所使用的给定物理连接器是否有效，并且如果一个或多个参数无效，应返回 E_INVALIDARG。

如果传递到 COPPCommand 的保护命令与监视器的显示分辨率不兼容，则 COPPCommand 应返回 DDERR_TOOBIGSIZE。

## <a name="mapping-rendermocomp-to-coppcommand"></a>将 RenderMoComp 映射到 COPPCommand

示例 COPPCommand 函数直接映射到对 DD_MOTIONCOMPCALLBACKS 结构的 RenderMoComp 成员的调用。 RenderMoComp 成员指向显示驱动程序提供的 DdMoCompRender 回调函数，该函数引用 DD_RENDERMOCOMPDATA 结构。

调用 RenderMoComp 回调函数时，不会首先调用显示驱动程序提供的 BeginMoCompFrame 或 EndMoCompFrame 函数。

按如下所示填充 DD_RENDERMOCOMPDATA 结构。

| 成员 | “值” |
| -- | -- |
| dwNumBuffers | Zero。 |
| lpBufferInfo | NULL。 |
| dwFunction | DXVA) 中定义 DXVA_COPPCommandFnCode 常量 (。|
| lpInputData | 指向 DXVA_COPPCommand 结构的指针。 |
| lpOutputData | NULL。 |

## <a name="example-code"></a>示例代码

下面的代码提供了一个示例，说明如何实现 COPPCommand 函数：

```cpp
GUID
COPP_CalculateMAC(
    AESHelper* pAesHelper,
    BYTE* pInputData,
    DWORD dwDataLength,
    GUID* pKDI
    )
{
    GUID rgbTag;
    memset(&rgbTag, 0, sizeof(GUID));
    SignData(pAesHelper, pInputData, dwDataLength, (BYTE*)&rgbTag);
    return rgbTag;
}

HRESULT
COPPCommand(
    COPP_DeviceData* pThis,
    DXVA_COPPCommand* pCommand
    )
{
    DXVA_COPPSetProtectionLevelCmdData CmdData;
    DWORD ProtIndex = COPP_ProtectionTypeIndex_Unkonwn;
    if (pThis->m_COPPDevState != COPP_SESSION_ACTIVE) {
        return E_UNEXPECTED;
    }
    if (pCommand->dwSequence != pThis->m_CmdSeqNumber) {
        return E_INVALIDARG;
    }
    if (!IsEqualGUID(&pCommand->guidCommandID, &DXVA_COPPSetProtectionLevel)) {
        return E_INVALIDARG;
    }
    //
    // ensure that enough data is passed
    //
    if (pCommand->cbSizeData < sizeof(DXVA_COPPSetProtectionLevelCmdData)) {
        return E_INVALIDARG;
    }
    //
    // verify that the command message was sent by the application
    // over the secure channel by validating the MAC on the message
    //
    GUID macCalculated = COPP_CalculateMAC(&pThis->m_AesHelper,
                                      (BYTE*)&pCommand->guidCommandID,
                              sizeof(DXVA_COPPCommand) - sizeof(GUID),
                                       &pThis->m_KDI);
        if (!IsEqualGUID(&macCalculated, &pCommand->macKDI)) {
            return E_UNEXPECTED;
        }
    memcpy(&CmdData, pCommand->CommandData, sizeof(DXVA_COPPSetProtectionLevelCmdData));
    //
    // determine which protection level (CmdData.ProtType) was passed and
    // set ProtIndex accordingly (for example, ProtIndex = COPP_ProtectionTypeIndex_ACP)
    //
    //
    // ensure that the request is valid
    //
    if (CmdData.ProtLevel >= g_nLevels[ProtIndex]) {
        return E_INVALIDARG;
    }
    // set the new local level and store the former local level
    DWORD oldLevel = pThis->m_LocalLevel[ProtIndex];
    pThis->m_LocalLevel[ProtIndex] = CmdData.ProtLevel;
    // decrement the former global level and increment the new
    g_COPPLevels[pThis->m_DevID].Levels[ProtIndex][oldLevel]--;
    g_COPPLevels[pThis->m_DevID].Levels[ProtIndex][CmdData.ProtLevel]++;
    pThis->m_CmdSeqNumber++;
    return NO_ERROR;
}
```

**惠?**

|目标平台 | 版本 |
| -- | -- |
| 台式机 | 此函数仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。 |



