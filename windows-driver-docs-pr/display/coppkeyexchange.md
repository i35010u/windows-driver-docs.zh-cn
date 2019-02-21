---
title: COPPKeyExchange 函数
description: 此示例 COPPKeyExchange 函数检索图形硬件使用的数字证书。
ms.assetid: ecf26fc7-fba0-4dcf-9b63-9808b8efec13
keywords:
- 复制保护 WDK COPP，微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，微型端口驱动程序代码模板
- 微型端口驱动程序 WDK Windows 2000，COPP 代码模板
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 14d2690e1f9387e02b327202a3d3a8df239a78ab
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544452"
---
# <a name="coppkeyexchange-function"></a>COPPKeyExchange 函数

此示例 COPPKeyExchange 函数检索图形硬件使用的数字证书。

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

* 指向 COPP DirectX VA 设备对象指针。

*pRandom [out]*

* 指向一个变量来接收一个 128 位随机数字。

*pGHCertificate [out]*

* 指向接收图形硬件证书字节的列表。

## <a name="return-value"></a>返回值

返回零 （S_OK 或 DD_OK） 如果成功，则否则，返回错误代码。

## <a name="remarks"></a>备注

接收到对其 COPPKeyExchange 函数的调用之前，COPP DirectX VA 设备应为 VMR 提供图形硬件证书的大小。 也就是说，COPPGetCertificateLength 函数应在 COPPKeyExchange 之前调用。 如果之前 COPPGetCertificateLength，将调用 COPPKeyExchange，COPPKeyExchange 应返回 E_UNEXPECTED。

## <a name="mapping-rendermocomp-to-coppkeyexchange"></a>映射到 COPPKeyExchange RenderMoComp

示例 COPPKeyExchange 函数直接映射到 DD_MOTIONCOMPCALLBACKS 结构的 RenderMoComp 成员调用。 RenderMoComp 成员指向显示驱动程序提供 DdMoCompRender 回调的函数的引用 DD_RENDERMOCOMPDATA 结构。

而无需显示驱动程序提供 BeginMoCompFrame 或 EndMoCompFrame 要调用的函数首先调用 RenderMoComp 回调函数。

按如下所示填充 DD_RENDERMOCOMPDATA 结构。

| 成员 | 值 |
|--|--|
| dwNumBuffers | 在 lpBufferInfo 的缓冲区数。 值为 1。 |
| lpBufferInfo | 指向一个 RGB32 系统内存图面，其中包含保存的硬件证书所需的空间。 对 COPPGetCertificateLength 的调用中返回的表面所需的长度。 <br>请注意，系统内存图面用于返回该证书，因为该证书的大小可以超过通过 lpOutputData 参数传递的最大缓冲区的大小。|
| dwFunction | DXVA_COPPKeyExchangeFnCode 常量 （dxva.h 中定义）。 |
| lpInputData | NULL。 |
| lpOutputData | 指向由驱动程序生成的 128 位随机数字。 |

## <a name="example-code"></a>示例代码

以下代码举例说明如何实现 COPPKeyExchange 函数：

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

**要求**

| 目标平台 | 版本 |
| -- | -- |
| 桌面设备 |  此函数仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。 |



