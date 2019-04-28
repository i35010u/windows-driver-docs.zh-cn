---
title: COPPCommand 函数
description: 示例 COPPCommand 函数执行 COPP DirectX VA 设备上的操作。
ms.assetid: 917628be-e965-4ca4-bfa8-0e80476df153
keywords:
- 复制保护 WDK COPP，微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，微型端口驱动程序代码模板
- 微型端口驱动程序 WDK Windows 2000，COPP 代码模板
- 已认证的输出保护协议
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 32d0be8fe821eb2beec0a0cb9064c635cfa2459d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331311"
---
# <a name="coppcommand-function"></a>COPPCommand 函数

示例 COPPCommand 函数执行 COPP DirectX VA 设备上的操作。

## <a name="syntax"></a>语法

```cpp
HRESULT COPPCommand(
  _In_ COPP_DeviceData  pThis,
  _In_ DXVA_COPPCommand *pCommand
);
```

## <a name="parameters"></a>Parameters

*pThis [in]*

 * 指向 COPP DirectX VA 设备对象指针。

*[in] pCommand*
* 提供了指向包含有关要 COPP 设备上执行的操作信息的 DXVA_COPPCommand 结构的指针。

## <a name="return-value"></a>返回值

返回零 （S_OK 或 DD_OK） 如果成功，则否则，返回错误代码。

## <a name="remarks"></a>备注

视频会话应设置为受保护模式 （即，它应处于活动状态） 关联 COPP DirectX VA 之前设备接收到对其 COPPCommand 函数的调用。 也就是说，COPPSequenceStart 函数应在 COPPCommand 之前调用。 如果之前 COPPSequenceStart，将调用 COPPCommand，COPPCommand 应返回 E_UNEXPECTED。

COPPCommand 函数接收包含 COPP 命令的填充的 DXVA_COPPCommand 结构。 支持以下 COPP 命令：

* **DXVA_COPPSetProtectionLevel** <br>视频的会话中的指令上的物理连接器设置保护级别与 COPP 设备相关联。 微型端口驱动程序应该能够支持多个视频会话所有播放通过同一个物理连接器返回内容。
* **DXVA_COPPSetSignaling** <br>有关如何保护信号，它们将通过与 DirectX VA COPP 设备相关联的物理连接器说明。

COPPCommand 函数应该验证传递给它的参数正在使用的给定物理连接器对有效，并应返回 E_INVALIDARG，如果一个或多个参数不是有效。

如果传递给 COPPCommand 保护命令是监视器的显示分辨率与不兼容，COPPCommand 应返回 DDERR_TOOBIGSIZE。

## <a name="mapping-rendermocomp-to-coppcommand"></a>映射到 COPPCommand RenderMoComp

示例 COPPCommand 函数直接映射到 DD_MOTIONCOMPCALLBACKS 结构的 RenderMoComp 成员调用。 RenderMoComp 成员指向显示驱动程序提供 DdMoCompRender 回调的函数的引用 DD_RENDERMOCOMPDATA 结构。

而无需显示驱动程序提供 BeginMoCompFrame 或 EndMoCompFrame 要调用的函数首先调用 RenderMoComp 回调函数。

按如下所示填充 DD_RENDERMOCOMPDATA 结构。

| 成员 | 值 |
| -- | -- |
| dwNumBuffers | 为零。 |
| lpBufferInfo | NULL。 |
| dwFunction | DXVA_COPPCommandFnCode 常量 （dxva.h 中定义）。|
| lpInputData | 指向 DXVA_COPPCommand 结构的指针。 |
| lpOutputData | NULL。 |

## <a name="example-code"></a>示例代码

以下代码举例说明如何实现 COPPCommand 函数：

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

**要求**

|目标平台 | Version |
| -- | -- |
| 桌面设备 | 此函数仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。 |



