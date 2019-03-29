---
title: EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR
description: EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR
ms.assetid: 5449A10A-17BC-40CB-A8FC-19F867CFC9D0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e4f5536405e92ac5b1b938f4c60389a09c92f051
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564837"
---
# <a name="efiusbsuperspeedendpointcompaniondescriptor"></a>EFI\_USB\_SUPERSPEED\_终结点\_配套\_描述符


**EFI\_USB\_SUPERSPEED\_终结点\_配套\_描述符**结构提供了对 USB 函数 SuperSpeed 终结点配套描述符驱动程序。

## <a name="syntax"></a>语法


```cpp
typedef struct
{
    UINT8          Length;
    UINT8          DescriptorType;
    UINT8          MaxBurst;
    union
    {
        UINT8      AsUchar;
        struct
        {
            UINT8  MaxStreams:5;
            UINT8  Reserved1:3;
        }          Bulk;
    }              Attributes;
    UINT16         BytesPerInterval;
} EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR;
```

## <a name="members"></a>成员


<a href="" id="length"></a>**长度**  
此说明符以字节为单位的大小。

<a href="" id="descriptortype"></a>**DescriptorType**  
指定的描述符类型。 必须设置为 SUPERSPEED\_USB\_终结点\_随附。

<a href="" id="maxburst"></a>**MaxBurst**  
数据包在终结点可以发送或接收一部分突然增加最大数目。

<a href="" id="asuchar"></a>**AsUchar**  
指定结构的长度。

<a href="" id="maxstreams"></a>**MaxStreams**  
指定流支持的大容量终结点的最大数目。

<a href="" id="reserved1"></a>**Reserved1**  
保留。 不使用。

<a href="" id="bytesperinterval"></a>**BytesPerInterval**  
总字节数的此终结点将传输每个服务重试间隔 (SI)。

## <a name="requirements"></a>要求


**标头：** 用户生成

 

 




