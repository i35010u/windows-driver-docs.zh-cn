---
title: COPPKeyExchange 函数
description: 示例 COPPKeyExchange 函数检索图形硬件使用的数字证书。
keywords:
- 复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，视频微型端口驱动程序代码模板
- 视频微型端口驱动程序 WDK Windows 2000，COPP 代码模板
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: e1c2bbe0bb4b235286ff282ee51713372d3ac3b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803577"
---
# <a name="coppkeyexchange-function"></a>COPPKeyExchange 函数

示例 COPPKeyExchange 函数检索图形硬件使用的数字证书。

### <a name="syntax"></a>语法

```cpp
HRESULT COPPKeyExchange(
  _In_  COPP_DeviceData pThis,
  _Out_ GUID            *pRandom,
  _Out_ BYTE            *pGHCertificate
);
```

## <a name="parameters"></a>参数

*pThis [in]*

* 指向 COPP DirectX VA 设备对象的指针。

*pRandom [out]*

* 指向接收128位随机数的变量的指针。

*pGHCertificate [out]*

* 一个指针，指向接收图形硬件证书的字节列表。

## <a name="return-value"></a>返回值

如果成功，则返回零 (S_OK 或 DD_OK) ;否则，将返回错误代码。

## <a name="remarks"></a>备注

COPP DirectX VA 设备应该先向 VMR 提供图形硬件证书的大小，然后才能接收对其 COPPKeyExchange 函数的调用。 也就是说，应在 COPPKeyExchange 之前调用 COPPGetCertificateLength 函数。 如果在 COPPGetCertificateLength 之前调用 COPPKeyExchange，则 COPPKeyExchange 应返回 E_UNEXPECTED。

## <a name="mapping-rendermocomp-to-coppkeyexchange"></a>将 RenderMoComp 映射到 COPPKeyExchange

示例 COPPKeyExchange 函数直接映射到对 DD_MOTIONCOMPCALLBACKS 结构的 RenderMoComp 成员的调用。 RenderMoComp 成员指向显示驱动程序提供的 DdMoCompRender 回调函数，该函数引用 DD_RENDERMOCOMPDATA 结构。

调用 RenderMoComp 回调函数时，不会首先调用显示驱动程序提供的 BeginMoCompFrame 或 EndMoCompFrame 函数。

按如下所示填充 DD_RENDERMOCOMPDATA 结构。

| 成员 | “值” |
|--|--|
| dwNumBuffers | LpBufferInfo 处的缓冲区数。 值为 1。 |
| lpBufferInfo | 指向单个 RGB32 系统内存的指针，其中包含持有硬件证书所需的空间。 在调用 COPPGetCertificateLength 时，将返回所需的图面长度。 <br>请注意，系统内存图面用于返回证书，因为证书的大小可以超过通过 lpOutputData 参数传递的最大缓冲区的大小。|
| dwFunction | DXVA) 中定义 DXVA_COPPKeyExchangeFnCode 常量 (。 |
| lpInputData | NULL。 |
| lpOutputData | 指向驱动程序生成的128位随机数的指针。 |

## <a name="example-code"></a>示例代码

下面的代码提供了一个示例，说明如何实现 COPPKeyExchange 函数：

```cpp
DWORD
COPP_Generate128BitRandomNumber()
{
    GUID RandNum;
    DWORD* pdw = (DWORD*)&RandNum;
    pdw[0] = rand();
    pdw[1] = rand();
    pdw[2] = rand();
    pdw[3] = rand();
    return RandNum;
}

HRESULT
COPPKeyExchange(
    COPP_DeviceData* pThis,
    GUID* pRandNumber,
    BYTE* pGHCertificate
    )
{
    if (pThis->m_COPPDevState != COPP_CERT_LENGTH_RETURNED) {
        return E_UNEXPECTED;
    }
    memcpy(pGHCertificate, (LPVOID)&TestCert, sizeof(TestCert));
    pThis->m_rGraphicsDriver = *pRandNumber = COPP_Generate128BitRandomNumber();
    pThis->m_COPPDevState = COPP_KEY_EXCHANGED;
    return NO_ERROR;
}
```

**惠?**

| 目标平台 | 版本 |
| -- | -- |
| 台式机 |  此函数仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。 |



