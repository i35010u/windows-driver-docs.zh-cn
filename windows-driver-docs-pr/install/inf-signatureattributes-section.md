---
title: INF SignatureAttributes 节
description: 此部分允许用户根据某些认证方案的要求请求其他签名。
ms.assetid: 8169686B-C45B-4D67-8B09-CD5F9977898D
keywords:
- INF SignatureAttributes 部分设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF SignatureAttributes Section
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9fb6ae4da095e1a830f4e0318d9d738de9bd026d
ms.sourcegitcommit: 5b0d2b7a3a4efa3bc4f94a769bf41d58d3321d50
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/16/2019
ms.locfileid: "72390720"
---
# <a name="inf-signatureattributes-section"></a>INF SignatureAttributes 节


此部分允许用户根据某些认证方案的要求请求其他签名。 例如，以下方案需要此部分：受保护的环境媒体播放、[初期启动反恶意软件](https://docs.microsoft.com/windows-hardware/drivers/install/elam-driver-submission)和第三方 HAL 扩展。 仅当硬件认证工具包包包含正确的功能并通过测试时才会应用这些附加签名。

```inf
[SignatureAttributes]
FileOne = SignatureAttributes.SigType

[SignatureAttributes.SigType]
Attribute = Value
```

## <a name="entries"></a>条目


<a href="" id="sigtype-signature-type"></a>**SigType =** <em>签名类型</em>  
定义需要将哪些签名或目录属性应用于文件。 应为以下各项之一：

-   Elam
-   HalExt
-   PETrust
-   DRM
-   WindowsHello

<a href="" id="attribute-attribute-name"></a>**Attribute =** <em>属性名称</em>  
每个签名类型都有相应的属性和值，如下所示。 将以下定义用于 SignatureAttributes 子节：

-   **SignatureAttributes. Elam**： Elam = true
-   **SignatureAttributes. HalExt**： HalExt = true
-   **SignatureAttributes**： DRMLevel = {1300 | 1200}
-   **SignatureAttributes. PETrust**： PETrust = true
-   **SignatureAttributes. WindowsHello**： WindowsHello = true

<a name="remarks"></a>备注
-------

仅当硬件认证工具包包包含正确的功能并通过测试时才会应用这些附加签名。 这些是硬件认证的正常行为以及 Elam、HalExt、PETrust 和 DRM 的相应认证要求的补充。 有关详细信息，请参阅[Windows 硬件实验室工具包](https://docs.microsoft.com/windows-hardware/test/hlk/)。

当请求其他签名时，应使用这些 INF 部分，而不考虑目标操作系统。

<a name="examples"></a>示例
--------

下面的示例演示如何枚举和请求音频的其他签名：

```inf
[SignatureAttributes]
ExampleFile1.dll=SignatureAttributes.PETrust
ExampleFile2.dll=SignatureAttributes.DRM

[SignatureAttributes.DRM]
DRMLevel=1300

 [SignatureAttributes.PETrust]
PETrust=true
```

下面的示例演示如何枚举和请求视频的其他签名：

```inf
[SignatureAttributes]
ExampleFile1.dll=SignatureAttributes.PETrust

[SignatureAttributes.PETrust]
PETrust=true
```

以下示例演示了如何枚举和请求 HAL 的其他签名：

```inf
[SignatureAttributes]
HALFILE.dll=SignatureAttributes.HalExt

[SignatureAttributes.HalExt]
HalExt=true
```

下面的示例演示如何枚举和请求 ELAM 的其他签名：

```inf
[SignatureAttributes]
ELAMFILE.dll=SignatureAttributes.Elam

[SignatureAttributes.Elam]
Elam=true
```

以下示例演示了如何枚举和请求 Windows Hello 的其他签名：

```inf
[SignatureAttributes]
WindowsHelloFile.dll=SignatureAttributes.WindowsHello

[SignatureAttributes.WindowsHello]
WindowsHello=true
```


## <a name="see-also"></a>另请参阅


[仪表板帮助](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)

 

 






