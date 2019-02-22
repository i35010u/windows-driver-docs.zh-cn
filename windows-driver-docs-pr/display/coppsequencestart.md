---
title: COPPSequenceStart 函数
description: 示例 COPPSequenceStart 函数将当前的视频会话设置为受保护模式。
ms.assetid: c3b3d4ad-ab86-4cc4-9023-8b0cd0655d42
keywords:
- 复制保护 WDK COPP，微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，微型端口驱动程序代码模板
- 微型端口驱动程序 WDK Windows 2000，COPP 代码模板
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0fa73c53c7b472bb2fe49b138e33de8c749a4af6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526495"
---
# <a name="coppsequencestart-function"></a>COPPSequenceStart 函数

示例 COPPSequenceStart 函数将当前的视频会话设置为受保护模式。

### <a name="syntax"></a>语法

```cpp
HRESULT COPPSequenceStart(
  _In_ COPP_DeviceData    pThis,
  _In_ DXVA_COPPSignature *pSeqStartInfo
);
```

## <a name="parameters"></a>参数

*pThis [in]*

* 指向 COPP DirectX VA 设备对象指针。

*pSeqStartInfo [in]*

* 提供了指向包含有关开始序列的信息的 DXVA_COPPSignature 结构的指针。

## <a name="return-value"></a>返回值

返回零 （S_OK 或 DD_OK） 如果成功，则否则，返回错误代码。

## <a name="remarks"></a>备注

接收到对其 COPPSequenceStart 函数的调用之前，COPP DirectX VA 设备应为 VMR 提供图形硬件证书。 也就是说，COPPKeyExchange 函数应在 COPPSequenceStart 之前调用。 如果之前 COPPKeyExchange，将调用 COPPSequenceStart，COPPSequenceStart 应返回 E_UNEXPECTED。

提供的图形硬件证书之后, COPP DirectX VA 设备应收到对其 COPPSequenceStart 函数只能有一个调用。 如果 COPP DirectX VA 设备收到另一个 COPPSequenceStart 调用，则应返回 E_UNEXPECTED。

COPPSequenceStart 函数接收包含开始序列，其中包括以下各项串联在一起的填充的 DXVA_COPPSignature 结构：

* 128 位随机数字生成由驱动程序并通过对驱动程序的 COPPKeyExchange 函数的调用返回
* 128 位随机数据完整性会话密钥
* 32 位随机起始状态序列号
* 32 位随机起始命令序列号

使用图形硬件的公钥进行加密开始序列。

## <a name="mapping-rendermocomp-to-coppsequencestart"></a>映射到 COPPSequenceStart RenderMoComp

示例 COPPSequenceStart 函数直接映射到 DD_MOTIONCOMPCALLBACKS 结构的 RenderMoComp 成员调用。 RenderMoComp 成员指向显示驱动程序提供 DdMoCompRender 回调的函数的引用 DD_RENDERMOCOMPDATA 结构。

而无需显示驱动程序提供 BeginMoCompFrame 或 EndMoCompFrame 要调用的函数首先调用 RenderMoComp 回调函数。

按如下所示填充 DD_RENDERMOCOMPDATA 结构。

| 成员 | 值 |
| -- | -- |
| dwNumBuffers | 为零。 |
| lpBufferInfo | NULL。 |
| dwFunction | DXVA_COPPSequenceStartFnCode 常量 （dxva.h 中定义）。 |
| lpInputData | 指向 DXVA_COPPSignature 结构的指针。 |
| lpOutputData | NULL。 |

## <a name="example-code"></a>示例代码

以下代码举例说明如何实现 COPPSequenceStart 函数：

```cpp
HRESULT
COPP_RSADecryptData(
    const BYTE* lpPrivateKey,
    DXVA_COPPSignature* pOutput,
    DXVA_COPPSignature* pInput
    )
{
    DWORD dwLen = sizeof(DXVA_COPPSignature);
    return RSADecPrivate(lpPrivateKey, (const BYTE *)pInput,
                         sizeof(DXVA_COPPSignature), (BYTE*) pOutput, &dwLen);
}

HRESULT
COPPSequenceStart(
    COPP_DeviceData* pThis,
    DXVA_COPPSignature* pSeqStartInfo
    )
{
    if (pThis->m_COPPDevState == COPP_KEY_EXCHANGED) {
        BYTE* pByte;
        DXVA_COPPSignature Decrypted;
        GUID rGraphicsDriver;
        HRESULT hr;
        COPP_RSADecryptData(PrivateKey, &Decrypted, pSeqStartInfo);
        pByte = (BYTE*)&Decrypted;
        memcpy(&rGraphicsDriver, pByte, sizeof(DWORD));
        pByte += sizeof(DWORD);
        memcpy(&pThis->m_KDI, pByte, sizeof(GUID));
        pByte += sizeof(GUID);
        memcpy(&pThis->m_StatusSeqNumber, pByte, sizeof(DWORD));
        pByte += sizeof(DWORD);
        memcpy(&pThis->m_CmdSeqNumber, pByte, sizeof(DWORD));
        pByte += sizeof(DWORD);
        hr = SetKey(&pThis->m_AesHelper, (BYTE*)&pThis->m_KDI, sizeof(GUID));
        if (hr != S_OK) {
            return hr;
        }
        if (!IsEqualGUID(&rGraphicsDriver, &pThis->m_rGraphicsDriver)) {
            return E_UNEXPECTED;
        }
        pThis->m_COPPDevState = COPP_SESSION_ACTIVE;
    }
    else {
        return E_UNEXPECTED;
    }
    return NO_ERROR;
}
```

**要求**

| 目标平台 | 版本 |
| -- | -- |
| 桌面设备 | 此函数仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。 |

