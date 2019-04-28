---
title: Bug 检查 0xF0 STORAGE_MINIPORT_ERROR
description: STORAGE_MINIPORT_ERROR bug 检查具有 0x00000F0 值。 它表示存储微型端口驱动程序无法完成 SRB 请求。
keywords:
- Bug 检查 0xF0 STORAGE_MINIPORT_ERROR
- STORAGE_MINIPORT_ERROR
ms.date: 01/24/2019
topic_type:
- apiref
api_name:
- STORAGE_MINIPORT_ERROR
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 34250b9e7efac7ed20071b28e7634417e18c4cf3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342115"
---
# <a name="bug-check-0xf0-storageminiporterror"></a>Bug 检查 0xF0：存储\_微型端口\_错误

存储\_微型端口\_错误 bug 检查的值为 0x00000F0。 它表示存储微型端口驱动程序无法完成 SRB 请求。


> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

 

## <a name="storageminiporterror-parameters"></a>存储\_微型端口\_错误参数

|参数|描述|
|-------- |---------- |
|1| 错误代码。 请参阅下面的值。|
|2| 请参阅下面的值。|
|3| 请参阅下面的值。|
|4| 请参阅下面的值。|

**值**

```text
1: Miniport failed to complete a SRB request even after successful reset operation.
    2 - Driver name unicode string address
    3 - SRB address
    4 - Storport unit device object

2: Miniport failed to complete a SRB request even after successful abort operation for the SRB.
    2 - Driver name unicode string address
    3 - Abort SRB address
    4 - SRB that was being aborted

3: Miniport failed to complete a request within a given timeout.
    2 - Driver name unicode string address
    3 - SRB address
    4 - Timeout of the request

4: Miniport failed to complete a request for a crypto operation. This can occur if it is trying to enable an encryption key on an ICE (Inline Crypto Engine) enabled UFS host. 
    2 - Driver name unicode string address
    3 - The STOR_CRYPTO_OPERATION_TYPE for this failure, typically StorCryptoOperationInsertKey
    4 - Reserved    
```


## <a name="cause"></a>原因
-----

存储微型端口驱动程序中的 bug 的完成保持 SRB 请求。 请参阅上面列出的特定类型的失败的错误代码值。


## <a name="resolution"></a>分辨率
-----

[！ 分析](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。 

返回参数 2 中的驱动程序名称应指向有问题的驱动程序。


## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

[Storport 的接口与 Storport 微型端口驱动程序](https://docs.microsoft.com/windows-hardware/drivers/storage/storport-s-interface-with-storport-miniport-drivers)

