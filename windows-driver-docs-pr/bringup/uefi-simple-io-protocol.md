---
title: UEFI 简单 I/O 协议
description: UEFI 简单 I/O 协议
ms.assetid: 0cb55bf5-71e9-4b59-aef1-7d74eb331a18
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 833dd66b6dcf8c302842bf6bcf542c0f1634b867
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56569289"
---
# <a name="uefi-simple-io-protocol"></a>UEFI 简单 I/O 协议


**请注意**  本部分中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

 

闪烁的工具使用简单的 I/O 协议以允许设备与预启动环境中的主机计算机之间进行通信。

**请注意**  将此文档的未来版本中提供有关闪烁的工具的信息。

 

## <a name="efisimplewinphoneioprotocol"></a>EFI\_简单\_WINPHONE\_IO\_协议


本部分提供的详细的说明**EFI\_简单\_WINPHONE\_IO\_协议**。 此协议使主机和预启动环境中的设备之间的简单通信。

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

**协议的接口结构**

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

<a href="" id="revision"></a>**修订版本**  
修订**EFI\_简单\_WINPHONE\_IO\_协议**遵循。 所有未来的版本必须是向后兼容。 如果将来的版本不是向后兼容，必须使用不同的 GUID。

<a href="" id="initialize"></a>**初始化**  
此函数将等待来自主机计算机的连接。 请参阅[EFI\_简单\_WINPHONE\_IO\_协议。初始化](efi-simple-winphone-io-protocolinitialize.md)。

<a href="" id="read"></a>**读取**  
从主计算机中接收的字节的缓冲区。 请参阅[EFI\_简单\_WINPHONE\_IO\_协议。读取](efi-simple-winphone-io-protocolread.md)。

<a href="" id="reserved-"></a>**保留**   
保留供将来使用。

<a href="" id="write"></a>**编写**  
向主机发送的字节的缓冲区。 请参阅[EFI\_简单\_WINPHONE\_IO\_协议。编写](efi-simple-winphone-io-protocolwrite.md)。

<a href="" id="getmaxpacketsize"></a>**GetMaxPacketSize**  
返回此协议支持的最大数据包大小。 请参阅[EFI\_简单\_WINPHONE\_IO\_协议。GetMaxPacketSize](efi-simple-winphone-io-protocolgetmaxpacketsize.md)。

