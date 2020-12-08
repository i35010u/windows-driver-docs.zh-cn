---
title: COPPSequenceStart 函数
description: 示例 COPPSequenceStart 函数将当前视频会话设置为受保护模式。
keywords:
- 复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，视频微型端口驱动程序代码模板
- 视频微型端口驱动程序 WDK Windows 2000，COPP 代码模板
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1d125203df8990ec020b5ea3dd7ad1ff31b32daa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826069"
---
# <a name="coppsequencestart-function"></a>COPPSequenceStart 函数

示例 COPPSequenceStart 函数将当前视频会话设置为受保护模式。

### <a name="syntax"></a>语法

```cpp
HRESULT COPPSequenceStart(
  _In_ COPP_DeviceData    pThis,
  _In_ DXVA_COPPSignature *pSeqStartInfo
);
```

## <a name="parameters"></a>参数

*pThis [in]*

* 指向 COPP DirectX VA 设备对象的指针。

*pSeqStartInfo [in]*

* 提供一个指向 DXVA_COPPSignature 结构的指针，该结构包含有关开始序列的信息。

## <a name="return-value"></a>返回值

如果成功，则返回零 (S_OK 或 DD_OK) ;否则，将返回错误代码。

## <a name="remarks"></a>备注

COPP DirectX VA 设备应该先向 VMR 提供图形硬件证书，然后才能接收对其 COPPSequenceStart 函数的调用。 也就是说，应在 COPPSequenceStart 之前调用 COPPKeyExchange 函数。 如果在 COPPKeyExchange 之前调用 COPPSequenceStart，则 COPPSequenceStart 应返回 E_UNEXPECTED。

提供图形硬件证书后，COPP DirectX VA 设备应该只接收一次对其 COPPSequenceStart 函数的调用。 如果 COPP DirectX VA 设备收到另一个 COPPSequenceStart 调用，它应返回 E_UNEXPECTED。

COPPSequenceStart 函数接收包含开始序列的已填充 DXVA_COPPSignature 结构，其中包含连接在一起的以下项：

* 128位随机数字，由驱动程序生成，通过对驱动程序的 COPPKeyExchange 函数的调用返回
* 128位随机数据完整性会话密钥
* 32位随机起始状态序列号
* 32位随机起始命令序列号

开始序列是使用图形硬件的公钥进行加密的。

## <a name="mapping-rendermocomp-to-coppsequencestart"></a>将 RenderMoComp 映射到 COPPSequenceStart

示例 COPPSequenceStart 函数直接映射到对 DD_MOTIONCOMPCALLBACKS 结构的 RenderMoComp 成员的调用。 RenderMoComp 成员指向显示驱动程序提供的 DdMoCompRender 回调函数，该函数引用 DD_RENDERMOCOMPDATA 结构。

调用 RenderMoComp 回调函数时，不会首先调用显示驱动程序提供的 BeginMoCompFrame 或 EndMoCompFrame 函数。

按如下所示填充 DD_RENDERMOCOMPDATA 结构。

| 成员 | “值” |
| -- | -- |
| dwNumBuffers | Zero。 |
| lpBufferInfo | NULL。 |
| dwFunction | DXVA) 中定义 DXVA_COPPSequenceStartFnCode 常量 (。 |
| lpInputData | 指向 DXVA_COPPSignature 结构的指针。 |
| lpOutputData | NULL。 |

## <a name="example-code"></a>示例代码

下面的代码提供了一个示例，说明如何实现 COPPSequenceStart 函数：

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

**惠?**

| 目标平台 | 版本 |
| -- | -- |
| 台式机 | 此函数仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。 |

