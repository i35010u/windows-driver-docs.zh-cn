---
title: UEFI 简单 I/O 协议
description: UEFI 简单 I/O 协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1a37e2588902435e3bcc90ccadf4bcffbf8affa8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806575"
---
# <a name="uefi-simple-io-protocol"></a>UEFI 简单 I/O 协议


**注意**  本节中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

 

使用简单的 i/o 协议，可以通过闪烁的工具在预启动环境中的设备和主机之间进行通信。

**注意**  此文档的未来版本中将提供有关闪烁工具的信息。

 

## <a name="efi_simple_winphone_io_protocol"></a>EFI \_ 简单 \_ WINPHONE \_ IO \_ 协议


本部分提供 **EFI \_ 简单 \_ WINPHONE \_ IO \_ 协议** 的详细说明。 此协议在预启动环境中启用主机和设备之间的简单通信。

**GUID**

```cpp
// {BDE900DD-190A-4c7d-9663-16BA8ED88B55}
#define EFI_SIMPLE_WINPHONE_IO_PROTOCOL_GUID \
  { 0xbde900dd, 0x190a, 0x4c7d, 0x96, 0x63, 0x16, 0xba, 0x8e, \
   0xd8, 0x8b, 0x55 };
```

**修订号**

```cpp
#define EFI_SIMPLE_WINPHONE_IO_PROTOCOL_REVISION   0x00010001
```

**协议接口结构**

```cpp
typedef struct _EFI_SIMPLE_WINPHONE_IO_PROTOCOL {
  UINT32                                        Revision;
  EFI_SIMPLE_WINPHONE_IO_INITIALIZE             Initialize;
  EFI_SIMPLE_WINPHONE_IO_READ                   Read;
  VOID*                                         Reserved;
  EFI_SIMPLE_WINPHONE_IO_WRITE                  Write;
  EFI_SIMPLE_WINPHONE_IO_GET_MAXPACKET_SIZE     GetMaxPacketSize;
} EFI_SIMPLE_WINPHONE_IO_PROTOCOL;
```

### <a name="members"></a>成员

<a href="" id="revision"></a>**A01**  
**EFI \_ 简单 \_ WINPHONE \_ IO \_ 协议** 遵循的修订版本。 所有将来的修订版都必须是向后兼容。 如果未来版本不是向后兼容的，则必须使用不同的 GUID。

<a href="" id="initialize"></a>**初始化**  
此函数等待主计算机的连接。 请参阅 [EFI \_ SIMPLE \_ WINPHONE \_ IO \_PROTOCOL.Initialize](efi-simple-winphone-io-protocolinitialize.md)。

<a href="" id="read"></a>**读取**  
从主计算机接收字节缓冲区。 请参阅 [EFI \_ SIMPLE \_ WINPHONE \_ IO \_ 协议。阅读](efi-simple-winphone-io-protocolread.md)。

<a href="" id="reserved-"></a>**保护**   
留待将来使用。

<a href="" id="write"></a>**写入**  
将字节缓冲区发送到主机计算机。 请参阅 [EFI \_ SIMPLE \_ WINPHONE \_ IO \_ 协议。写](efi-simple-winphone-io-protocolwrite.md)。

<a href="" id="getmaxpacketsize"></a>**GetMaxPacketSize**  
返回此协议支持的最大数据包大小。 请参阅 [EFI \_ SIMPLE \_ WINPHONE \_ IO \_ 协议。GetMaxPacketSize](efi-simple-winphone-io-protocolgetmaxpacketsize.md)。

