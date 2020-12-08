---
title: COPPGetCertificateLength 函数
description: 示例 COPPGetCertificateLength 函数检索图形硬件使用的证书的大小（以字节为单位）。
keywords:
- 复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，视频微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，视频微型端口驱动程序代码模板
- 视频微型端口驱动程序 WDK Windows 2000，COPP 代码模板
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3ed3d9e357835e5dc6c5c4d8729f487f81b51942
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787533"
---
# <a name="coppgetcertificatelength-function"></a>COPPGetCertificateLength 函数

示例 COPPGetCertificateLength 函数检索图形硬件使用的证书的大小（以字节为单位）。

### <a name="syntax"></a>语法

```cpp
HRESULT COPPGetCertificateLength(
  _In_  COPP_DeviceData pThis,
  _Out_ ULONG           *pCertificateLength
);
```

## <a name="parameters"></a>参数

*pThis [in]*

* 指向 COPP DirectX VA 设备对象的指针。

*pCertificateLength [out]*

* 指向一个变量的指针，该变量接收图形硬件使用的证书的大小（以字节为单位）。

## <a name="return-value"></a>返回值

如果成功，则返回零 (S_OK 或 DD_OK) ;否则，将返回错误代码。

## <a name="remarks"></a>备注

COPP DirectX VA 设备应该在接收对其 COPPGetCertificateLength 函数的调用之前进行初始化。 也就是说，应在 COPPGetCertificateLength 之前调用 COPPOpenVideoSession 函数。 如果在 COPPOpenVideoSession 之前调用 COPPGetCertificateLength，则 COPPGetCertificateLength 应返回 E_UNEXPECTED。

## <a name="mapping-rendermocomp-to-coppgetcertificatelength"></a>将 RenderMoComp 映射到 COPPGetCertificateLength

示例 COPPGetCertificateLength 函数直接映射到对 DD_MOTIONCOMPCALLBACKS 结构的 RenderMoComp 成员的调用。 RenderMoComp 成员指向显示驱动程序提供的 DdMoCompRender 回调函数，该函数引用 DD_RENDERMOCOMPDATA 结构。

调用 RenderMoComp 回调函数时，不会首先调用显示驱动程序提供的 BeginMoCompFrame 或 EndMoCompFrame 函数。

按如下所示填充 DD_RENDERMOCOMPDATA 结构。

| 成员 | “值” |
| -- | -- |
| dwNumBuffers | Zero。 |
| lpBufferInfo | NULL。 |
| dwFunction | DXVA) 中定义 DXVA_COPPGetCertificateLengthFnCode 常量 (。 |
| lpInputData | NULL。 |
| lpOutputData | 指向 ULONG 类型化变量的指针。 |

## <a name="example-code"></a>示例代码

下面的代码提供了一个示例，说明如何实现 COPPGetCertificateLength 函数：

```cpp
HRESULT
COPPGetCertificateLength(
    COPP_DeviceData* pThis,
    DWORD* pCertificateLength
    )
{
    if (pThis->m_COPPDevState != COPP_OPENED) {
        return E_UNEXPECTED;
    }
    *pCertificateLength = sizeof(TestCert);
    pThis->m_COPPDevState = COPP_CERT_LENGTH_RETURNED;
    return NO_ERROR;
}
```

**惠?**

| 目标平台 | 版本 |
| -- | -- |
| 台式机 | 此函数仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。 |



