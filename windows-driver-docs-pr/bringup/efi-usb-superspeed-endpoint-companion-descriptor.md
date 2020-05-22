---
title: EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR
description: EFI_USB_SUPERSPEED_ENDPOINT_COMPANION_DESCRIPTOR
ms.assetid: 5449A10A-17BC-40CB-A8FC-19F867CFC9D0
ms.date: 05/21/2020
ms.localizationpriority: medium
ms.openlocfilehash: e7e6e3d081ecb3a815a965d5773cf9a99330d281
ms.sourcegitcommit: 34a06eda78c8d935f3900b86fa0f620027bc6577
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/22/2020
ms.locfileid: "83778333"
---
# <a name="efi_usb_superspeed_endpoint_companion_descriptor"></a>EFI \_ USB \_ SUPERSPEED \_ 终结点 \_ 伴随 \_ 描述符

**EFI \_ usb \_ SUPERSPEED \_ 终结点 \_ 伴随 \_ 描述符**结构提供 USB 函数驱动程序的 SUPERSPEED 终结点伴随描述符。

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

### <a name="length"></a>长度

此描述符的大小（以字节为单位）。

### <a name="descriptortype"></a>DescriptorType

指定描述符类型。 必须设置为 SUPERSPEED \_ USB \_ 终结点 \_ 随附的。

### <a name="maxburst"></a>MaxBurst

终结点作为突发过程的一部分可以发送或接收的数据包的最大数量。

### <a name="asuchar"></a>AsUchar

指定结构的长度。

### <a name="maxstreams"></a>MaxStreams

指定大容量终结点支持的最大流数。

### <a name="reserved1"></a>Reserved1

保留。 请勿使用。

### <a name="bytesperinterval"></a>BytesPerInterval

此终结点将每个服务间隔（SI）传输的总字节数。

## <a name="requirements"></a>要求

**标头：** 用户生成
