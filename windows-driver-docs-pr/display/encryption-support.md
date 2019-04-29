---
title: 加密支持
description: 加密支持
ms.assetid: d5ce9c02-7126-4775-bb87-dae45b93b652
keywords:
- 视频解码 WDK DirectX VA 加密
- 解码视频 WDK DirectX VA 加密
- 图片解码 WDK DirectX VA 加密
- 加密 WDK DirectX VA
- 加密 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a7e1139a12c829ab8f6f5f324d1b93a8b299c13
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380414"
---
# <a name="encryption-support"></a>加密支持


## <span id="ddk_encryption_support_gg"></span><span id="DDK_ENCRYPTION_SUPPORT_GG"></span>


视频解码中使用的数据可以为以下结构和类型的数据进行加密：

-   宏块控制命令结构

-   残差差异块结构

-   位流缓冲区

为了使主机解码器使用加密，它必须确定哪些类型的加密快捷键支持。 有关支持的加速器的加密类型的信息包含在视频加速器格式的 Guid 作为到主机提供的加密类型 Guid 列表。 有关视频加速器格式的 Guid 的详细信息，请参阅 Microsoft Windows SDK 文档。

**请注意**  所有 DirectX VA 加速器必须都都能够运行，无需使用加密。 支持运行没有加密，因此，不需要声明，以及 DXVA\_NoEncrypt"不加密"GUID 必须永远不会发送视频加速器格式 GUID 列表中。

 

主机选择要应用的加密协议的类型，并指示此选择通过发送给快捷键的 GUID。 在典型的加密方案中，两个步骤之前进行加密的数据可以成功传输：

1.  主机解码器可能需要验证快捷键有权接收的数据。 可以通过将已签名的结构传递到主机以证明它保留的已授权的公钥/私钥对的加速器提供此验证。

2.  然后，主机解码器将加密的内容密钥发送给快捷键。

用于初始化加密协议的步骤的精确数量取决于正在使用的加密类型和实现方式。

每个主机和加速器将初始化参数传递必要的加密之间交换的数据集必须以加密协议类型 GUID 为前缀。 此 GUID 可区分的一种类型的另一种从数据加密的数据。 这是加密的必需的因为无法对一个 DirectX VA 缓冲区，使用一种类型和加密的另一种可以用于对另一个 DirectX VA 缓冲区。

[ **DXVA\_EncryptProtocolHeader** ](https://msdn.microsoft.com/library/windows/hardware/ff563965)结构用于指示正在使用加密协议以及正在使用的加密类型。

 

 





