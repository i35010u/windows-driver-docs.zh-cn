---
title: COPPGetCertificateLength 函数
description: 此示例 COPPGetCertificateLength 函数检索大小 （字节） 使用图形硬件的证书。
ms.assetid: 4a043c47-a5d2-4a7e-911c-9f57f7aa82cf
keywords:
- 复制保护 WDK COPP，微型端口驱动程序代码模板
- 视频复制保护 WDK COPP，微型端口驱动程序代码模板
- 受保护的视频 WDK COPP，微型端口驱动程序代码模板
- 微型端口驱动程序 WDK Windows 2000，COPP 代码模板
ms.date: 02/16/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7d162c85630794490ae4596b2a4cab151370e002
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523158"
---
# <a name="coppgetcertificatelength-function"></a>COPPGetCertificateLength 函数

此示例 COPPGetCertificateLength 函数检索大小 （字节） 使用图形硬件的证书。

### <a name="syntax"></a>语法

```cpp
HRESULT COPPGetCertificateLength(
  _In_  COPP_DeviceData pThis,
  _Out_ ULONG           *pCertificateLength
);
```

## <a name="parameters"></a>参数

*pThis [in]*

* 指向 COPP DirectX VA 设备对象指针。

*pCertificateLength [out]*

* 指向一个变量来接收大小，以字节为单位的图形硬件使用的证书。

## <a name="return-value"></a>返回值

返回零 （S_OK 或 DD_OK） 如果成功，则否则，返回错误代码。

## <a name="remarks"></a>备注

COPP DirectX VA 设备应接收到对其 COPPGetCertificateLength 函数的调用之前已初始化。 也就是说，COPPOpenVideoSession 函数应在 COPPGetCertificateLength 之前调用。 如果之前 COPPOpenVideoSession，将调用 COPPGetCertificateLength，COPPGetCertificateLength 应返回 E_UNEXPECTED。

## <a name="mapping-rendermocomp-to-coppgetcertificatelength"></a>映射到 COPPGetCertificateLength RenderMoComp

示例 COPPGetCertificateLength 函数直接映射到 DD_MOTIONCOMPCALLBACKS 结构的 RenderMoComp 成员调用。 RenderMoComp 成员指向显示驱动程序提供 DdMoCompRender 回调的函数的引用 DD_RENDERMOCOMPDATA 结构。

而无需显示驱动程序提供 BeginMoCompFrame 或 EndMoCompFrame 要调用的函数首先调用 RenderMoComp 回调函数。

按如下所示填充 DD_RENDERMOCOMPDATA 结构。

| 成员 | 值 |
| -- | -- |
| dwNumBuffers | 为零。 |
| lpBufferInfo | NULL。 |
| dwFunction | DXVA_COPPGetCertificateLengthFnCode 常量 （dxva.h 中定义）。 |
| lpInputData | NULL。 |
| lpOutputData | 指向 ULONG 类型的变量。 |

## <a name="example-code"></a>示例代码

以下代码举例说明如何实现 COPPGetCertificateLength 函数：

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

**要求**

| 目标平台 | 版本 |
| -- | -- |
| 桌面设备 | 此函数仅适用于 Windows Server 2003 SP1 和更高版本和 Windows XP SP2 和更高版本。 |



