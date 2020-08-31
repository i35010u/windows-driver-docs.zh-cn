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
ms.openlocfilehash: 3b354d0c1ec63eee31947f2dcba5fcfde07fa5df
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067126"
---
# <a name="using-crypto-session-with-directx-video-accelerator-20-decoder"></a>将加密会话与 DirectX 视频加速器 2.0 解码器配合使用


本部分仅适用于 Windows 7 和更高版本，以及 windows Server 2008 R2 及更高版本的 Windows 操作系统。

用户模式显示驱动程序可以将加密会话与 (VA) 2.0 解码设备的 DirectX 视频加速器相关联，以使 DirectX VA 2.0 解码设备使用加密会话的会话密钥。 如果在运行时调用驱动程序的[**CREATECRYPTOSESSION**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createcryptosession)函数以创建加密会话时，Direct3D 运行时在[**D3DDDIARG \_ CREATECRYPTOSESSION**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_createcryptosession)结构的**DecodeProfile**成员中指定了有效的解码 GUID，则运行时可以随后调用驱动程序的[**ConfigureAuthenticatedChannel**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_configureauthenicatedchannel)函数，其中 D3DAUTHETICATEDCONFIGURE CRYPTOSESSION \_ 设置为使用 DirectX VA 2.0 解码设备配置加密会话。 在使用 DirectX VA 2.0 解码设备配置加密会话之前，运行时必须调用驱动程序的 [**DecodeExtensionExecute**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeextensionexecute) 函数来检索 DirectX va 2.0 解码设备的驱动程序句柄。 运行时将 [**D3DDDIARG \_ DECODEEXTENSIONEXECUTE**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodeextensionexecute) 结构的成员设置为以下值，以检索 DirectX VA 2.0 解码设备的驱动程序句柄：

```cpp
#define DXVA2_DECODE_GET_DRIVER_HANDLE    0x725
D3DDDIARG_DECODEEXTENSIONEXECUTE.Function = DXVA2_DECODE_GET_DRIVER_HANDLE;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->pData = NULL;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->DataSize = 0;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->pData = HANDLE*;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->DataSize = sizeof(HANDLE);
```

当运行时调用驱动程序的 [**CreateDecodeDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdecodedevice) 函数来创建 DirectX VA 2.0 解码设备时，运行时在 [**DXVADDI \_ CONFIGPICTUREDECODE**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_configpicturedecode) 结构内为解码加密 guid 指定零。

在运行时调用驱动程序的[**CreateCryptoSession**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createcryptosession)函数，并将[**D3DDDIARG \_ CreateCryptoSession**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_createcryptosession)结构的**CryptoType**成员设置为 D3DCRYPTOTYPE \_ AES128 \_ CTR 来创建加密会话后，在对驱动程序的[**PPVPSetKey**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodebeginframe)函数的调用中，D3DDDIARG [** \_ DECODEBEGINFRAME**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodebeginframe)结构的**DECODEBEGINFRAME**成员的设置用于对帧进行解码，这表示以下含义：

-   如果将 **pPVPSetKey** 设置为 **NULL**，则不会有该帧的任何缓冲区包含加密数据，因此不需要解密。

-   如果 **pPVPSetKey** 指向空 \_ GUID (全部为零) ，则将用会话密钥对帧的缓冲区进行加密。

-   如果 **pPVPSetKey** 指向内容密钥，则表示应用程序使用了会话密钥来加密内容密钥。 驱动程序应使用此内容密钥来解密与此帧关联的所有加密缓冲区。

每个加密缓冲区的初始化向量出现在对驱动程序的[**DecodeExecute**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeexecute)函数的调用中的[**DXVADDI \_ DECODEBUFFERDESC**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_decodebufferdesc)结构的**pCipherCounter**成员中。 如果该驱动程序确定以前为同一内容密钥使用了初始化向量 (或会话密钥（如果未) 内容密钥），则该驱动程序应将对其 *DecodeExecute* 函数的调用失败。 应用程序应为应用程序加密的每个缓冲区增加[**DXVADDI \_ PVP \_ HW \_ iv**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_dxvaddi_pvp_hw_iv)的**iv**成员。 因此，如果**IV**成员小于或等于传递到*DecodeExecute*的以前的**iv**值，则驱动程序的*DecodeExecute*函数可能会失败。

如果运行时必须对缓冲区进行部分加密，它将调用驱动程序的 [**DecodeExtensionExecute**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_decodeextensionexecute) 函数，并将 [**D3DDDIARG \_ DecodeExtensionExecute**](/windows-hardware/drivers/ddi/d3dumddi/ns-d3dumddi-_d3dddiarg_decodeextensionexecute) 结构的成员设置为以下值，以指定驱动程序应加密的块：

```cpp
#define DXVA2_DECODE_SPECIFY_ENCRYPTED_BLOCKS    0x724
D3DDDIARG_DECODEEXTENSIONEXECUTE.Function = DXVA2_DECODE_SPECIFY_ENCRYPTED_BLOCKS;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->pData = D3DENCRYPTED_BLOCK_INFO*;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateInput->DataSize = sizeof(D3DENCRYPTED_BLOCK_INFO);
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->pData = NULL;
D3DDDIARG_DECODEEXTENSIONEXECUTE.pPrivateOutput->DataSize = 0;
```

 

