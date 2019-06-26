---
title: INF SignatureAttributes 节
description: 此部分允许用户请求所需的某些证书方案的其他签名。
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
ms.openlocfilehash: 02883650cb3b47982d07f5f76b52b90432a621da
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67370035"
---
# <a name="inf-signatureattributes-section"></a>INF SignatureAttributes 节


此部分允许用户请求所需的某些证书方案的其他签名。 例如，下面的方案需要此部分：受保护的环境媒体播放[早期启动反恶意软件](https://docs.microsoft.com/windows-hardware/drivers/install/elam-driver-submission)，和第三方 HAL 扩展。 如果您的硬件认证工具包程序包包含正确的功能，通过测试，将只应用这些附加的签名。

```inf
[SignatureAttributes]
FileOne = SignatureAttributes.SigType

[SignatureAttributes.SigType]
Attribute = Value
```

## <a name="entries"></a>条目


<a href="" id="sigtype-signature-type"></a>**SigType=** <em>signature-type</em>  
定义要应用于该文件的签名或目录属性需求。 应为以下值之一：

-   Elam
-   HalExt
-   PETrust
-   DRM
-   WindowsHello

<a href="" id="attribute-attribute-name"></a>**Attribute=** <em>attribute-name</em>  
每个签名类型都有相应的属性和值，如下所示。 使用这些定义 SignatureAttributes 各小节：

-   **SignatureAttributes.Elam**:Elam = true
-   **SignatureAttributes.HalExt**:HalExt = true
-   **SignatureAttributes.DRM**:DRMLevel = {1300年 | 1200年}
-   **SignatureAttributes.PETrust**:PETrust = true
-   **SignatureAttributes.WindowsHello**:WindowsHello = true

<a name="remarks"></a>备注
-------

如果您的硬件认证工具包程序包包含正确的功能，通过测试，将只应用这些附加的签名。 这些是正常行为的硬件认证和 Elam、 HalExt、 PETrust，相应的证书要求的添加项，详情请参阅 DRM[此处](https://go.microsoft.com/fwlink/p/?linkid=239763)。

请求而不考虑目标操作系统的附加签名时，应使用这些 INF 部分。

<a name="examples"></a>示例
--------

以下示例演示如何枚举和请求附加签名音频：

```inf
[SignatureAttributes]
ExampleFile1.dll=SignatureAttributes.PETrust
ExampleFile2.dll=SignatureAttributes.DRM

[SignatureAttributes.DRM]
DRMLevel=1300

 [SignatureAttributes.PETrust]
PETrust=true
```

以下示例演示如何枚举和请求视频附加签名：

```inf
[SignatureAttributes]
ExampleFile1.dll=SignatureAttributes.PETrust

[SignatureAttributes.PETrust]
PETrust=true
```

以下示例演示如何枚举和为 HAL 请求附加签名：

```inf
[SignatureAttributes]
HALFILE.dll=SignatureAttributes.HalExt

[SignatureAttributes.HalExt]
HalExt=true
```

以下示例演示如何枚举和请求的 ELAM 附加签名：

```inf
[SignatureAttributes]
ELAMFILE.dll=SignatureAttributes.Elam

[SignatureAttributes.Elam]
Elam=true
```

以下示例演示如何枚举和 Windows hello 企业请求附加签名：

```inf
[SignatureAttributes]
WindowsHelloFile.dll=SignatureAttributes.WindowsHello

[SignatureAttributes.WindowsHello]
WindowsHello=true
```


## <a name="see-also"></a>请参阅


[仪表板帮助](https://docs.microsoft.com/windows-hardware/drivers/dashboard/)

 

 






