---
title: 将加密会话用于 DXVA 2.0 解码器
description: 将加密会话与 DirectX 视频加速器 2.0 解码器配合使用
ms.assetid: 2a3577f5-bc44-4e0d-a5fa-217dc6c6f5f3
keywords:
- DXVA 2.0 解码器 WDK Windows 7 显示
- DXVA 2.0 解码器 WDK Windows Server 2008 R2 显示
- DXVA 2.0 解码器 WDK Windows 7 显示，与加密会话关联
- DXVA 2.0 解码器 WDK Windows Server 2008 R2 显示，与加密会话关联
- DirectX 视频加速器2.0 解码器 WDK Windows 7 显示
- DirectX 视频加速器2.0 解码器 WDK Windows Server 2008 R2 显示
- DirectX 视频加速器2.0 解码器 WDK Windows 7 显示，与加密会话关联
- DirectX 视频加速器2.0 解码器 WDK Windows Server 2008 R2 显示，与加密会话关联
- 加密会话 WDK Windows 7 显示
- 加密会话 WDK Windows Server 2008 R2 显示
- 加密会话 WDK Windows 7 显示，与 DXVA 2.0 解码器关联
- 加密会话 WDK Windows Server 2008 R2 显示，与 DXVA 2.0 解码器关联
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: da1d0b85f66f22fa247d4520a6b453ed750c4400
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72825391"
---
# <a name="using-crypto-session-with-directx-video-accelerator-20-decoder"></a>将加密会话与 DirectX 视频加速器 2.0 解码器配合使用


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

用户模式显示驱动程序可以将加密会话与 DirectX 视频加速器（VA）2.0 解码设备关联，以使 DirectX VA 2.0 解码设备使用加密会话的会话密钥。 如果在运行时调用驱动程序的[**CREATECRYPTOSESSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createcryptosession)函数创建加密时，Direct3D 运行时在[**D3DDDIARG\_CREATECRYPTOSESSION**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_createcryptosession)结构的**DecodeProfile**成员中指定有效解码 GUID会话后，运行时可以随后调用驱动程序的[**ConfigureAuthenticatedChannel**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_configureauthenicatedchannel)函数，并将 D3DAUTHETICATEDCONFIGURE\_CRYPTOSESSION 设置为，以配置包含 DirectX VA 2.0 解码设备的加密会话。 在使用 DirectX VA 2.0 解码设备配置加密会话之前，运行时必须调用驱动程序的[**DecodeExtensionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeextensionexecute)函数来检索 DirectX va 2.0 解码设备的驱动程序句柄。 运行时将[**D3DDDIARG\_DECODEEXTENSIONEXECUTE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodeextensionexecute)结构的成员设置为以下值，以检索 DirectX VA 2.0 解码设备的驱动程序句柄：

```cpp
#define DXVA2_DECODE_GET_DRIVER_HANDLE    0x725
D3DDDIARG_DECODEEXTENSIONEXECUTE.Function = DXVA2_DECODE_GET_DRIVER_HANDLE;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->pData = NULL;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->DataSize = 0;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->pData = HANDLE*;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->DataSize = sizeof(HANDLE);
```

当运行时调用驱动程序的[**CreateDecodeDevice**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdecodedevice)函数来创建 DirectX VA 2.0 解码设备时，运行时将为[**DXVADDI\_CONFIGPICTUREDECODE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_configpicturedecode)结构中的解码加密 guid 指定零。

在运行时调用驱动程序的[**CreateCryptoSession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createcryptosession)函数，并将[**D3DDDIARG\_CreateCryptoSession**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_createcryptosession)结构的**CryptoType**成员设置为 D3DCRYPTOTYPE\_AES128\_CTR 来创建加密会话，对驱动程序的[**DECODEBEGINFRAME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodebeginframe)函数进行调用以对帧进行解码时， [**D3DDDIARG\_DECODEBEGINFRAME**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodebeginframe)结构的**pPVPSetKey**成员的设置指示以下含义：

-   如果将**pPVPSetKey**设置为**NULL**，则不会有该帧的任何缓冲区包含加密数据，因此不需要解密。

-   如果**pPVPSetKey**指向 NULL\_GUID （所有零），则将用会话密钥对帧的缓冲区进行加密。

-   如果**pPVPSetKey**指向内容密钥，则表示应用程序使用了会话密钥来加密内容密钥。 驱动程序应使用此内容密钥来解密与此帧关联的所有加密缓冲区。

每个加密缓冲区的初始化向量出现在对驱动程序的[**DecodeExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeexecute)函数的调用中， [**DXVADDI\_DECODEBUFFERDESC**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_decodebufferdesc)结构的**pCipherCounter**成员中。 如果驱动程序确定先前已将初始化向量用于同一内容密钥（如果未使用内容密钥，则为会话密钥），则该驱动程序应将对其*DecodeExecute*函数的调用失败。 应用程序应将 DXVADDI\_PVP 的**iv**成员与应用程序加密的每个缓冲区[ **\_HW\_iv**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_pvp_hw_iv)递增。 因此，如果**IV**成员小于或等于传递到*DecodeExecute*的以前的**iv**值，则驱动程序的*DecodeExecute*函数可能会失败。

如果运行时必须对缓冲区进行部分加密，它将调用驱动程序的[**DecodeExtensionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeextensionexecute)函数，并将[**D3DDDIARG\_DecodeExtensionExecute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodeextensionexecute)结构的成员设置为以下值，以指定哪些块驱动程序应加密：

```cpp
#define DXVA2_DECODE_SPECIFY_ENCRYPTED_BLOCKS    0x724
D3DDDIARG_DECODEEXTENSIONEXECUTE.Function = DXVA2_DECODE_SPECIFY_ENCRYPTED_BLOCKS;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->pData = D3DENCRYPTED_BLOCK_INFO*;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->DataSize = sizeof(D3DENCRYPTED_BLOCK_INFO);
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->pData = NULL;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->DataSize = 0;
```

 

 





