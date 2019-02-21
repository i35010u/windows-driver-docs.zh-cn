---
title: 通信的高清晰度音频编解码器的谓词
description: 通信的高清晰度音频编解码器的谓词
ms.assetid: d93013fa-5b09-4616-bc71-5d3838337717
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 71f8ec7ff40cd04a6236fef85a75b933365a78b8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546716"
---
# <a name="communicating-verbs-with-the-hd-audio-codec"></a>通信的高清晰度音频编解码器的谓词


IOCTL\_AZALIABUS\_SENDVERBS IOCTL 由 Hdau.exe pin 配置工具时为音频适配器定义声音的拓扑。 请不要将此 IOCTL 用于其他目的。 此信息 IOCTL\_AZALIABUS\_SENDVERBS 提供其设计和实施仅记录。 Windows 7 Hdaudio.sys 音频类驱动程序支持此 IOCTL。

高清晰度 (HD) 音频编解码器都能够接收和响应的谓词。 作为的一部分说明了这些谓词和对这些谓词的响应的编解码器[HD 音频规范](https://go.microsoft.com/fwlink/p/?linkid=169394)。

在 Windows 7 和更高版本的 Windows 操作系统，HD 音频类驱动程序将使用 IOCTL\_AZALIABUS\_SENDVERBS IOCTL 进行通信的音频编解码器的谓词。 IOCTL\_AZALIABUS\_SENDVERBS 定义如下面的示例中所示：

```cpp
#define IOCTL_AZALIABUS_SENDVERBS CTL_CODE(FILE_DEVICE_UNKNOWN, 1, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

有关文件的详细信息\_设备\_未知，则方法\_缓冲，并且文件\_ANY\_访问权限，请参阅 Windows SDK 中的 Devioctl.h 标头文件。

若要启动与音频编解码器的通信，在类驱动程序调用[DeviceIoControl](https://go.microsoft.com/fwlink/p/?linkid=124239)使用以下参数的函数。

```cpp
BOOL DeviceIoControl(
  (HANDLE) hDevice,                      // handle to device
  IOCTL_AZALIABUS_SENDVERBS,             // dwIoControlCode
  NULL,                                  // lpInBuffer
  0,                                     // nInBufferSize
  (LPVOID) lpOutBuffer,                  // output buffer
  (DWORD) nOutBufferSize,                // size of output buffer
  (LPDWORD) lpBytesReturned,             // number of bytes returned
  (LPOVERLAPPED) lpOverlapped            // OVERLAPPED structure
);
```

如果在调用[ **DeviceIoControl** ](https://msdn.microsoft.com/library/windows/desktop/aa363216)是成功，它将返回一个非零值。 如果调用失败或被挂起 （不立即处理）， **DeviceIoControl**返回零值。 在类驱动程序可以调用[GetLastError](https://go.microsoft.com/fwlink/p/?linkid=169416)的更详细的错误消息。

当音频驱动程序必须更改 pin 配置默认值时，它可以使用 IOCTL\_AZALIABUS\_SENDVERBS 发送和接收设置和获取从音频编解码器的谓词。 如果与音频编解码器的通信不是 pin 配置中，音频编解码器将仅响应 Get 谓词。

下面的示例演示使用 AzCorbeEntry 结构和句柄作为参数并返回 AzRirbResponse 从编解码器的函数。

```cpp
AzRirbEntry SendVerb(HANDLE handle, AzCorbEntry verb)
{
  UserModeCodecCommandPacket c;
  UserModeCodecResponsePacket r;
  c.NumCommands = 1;
  c.Command[0] = verb;
  DWORD BytesReturned;

//A nonzero value is returned for a successful call and it is interpreted as TRUE  
BOOL rc = DeviceIoControl(handle, IOCTL_AZALIABUS_SENDVERBS, &c, sizeof(c), &r, sizeof(r), &BytesReturned, 0);

  if(!rc)
  {
    printf("Failed to communicate with the device!\n");
    return 0;
  }

  if(BytesReturned != sizeof(r))
  {
    printf("Wrong number of bytes returned!\n");
    return 0;
  }

  return r.Response[0];
}
```

在下面的示例定义了数据类型和在前面的代码示例中使用的结构：

### <a name="span-idazcorbentryspanspan-idazcorbentryspan-azcorbentry"></a><span id="azcorbentry"></span><span id="AZCORBENTRY"></span> AzCorbEntry

```cpp
struct AzCorbEntry
{
  ULONG Verb        : 20; // 0:19
  ULONG NodeId      : 7;  // 20:26
  ULONG IndirectNID : 1;  // 27
  ULONG LinkId      : 4;  // 28:31
  enum {Invalid = 0xffffffff};
  AzCorbEntry(ULONG x = 0)
  :
    Verb(x),
    NodeId(x >> 20),
    IndirectNID(x >> 27),
    LinkId(x >> 28) {}
  operator ULONG()
  {
    return Verb | NodeId << 20 | IndirectNID << 27 | LinkId << 28;
  }
};
```

### <a name="span-idazrirbentryspanspan-idazrirbentryspan-azrirbentry"></a><span id="azrirbentry"></span><span id="AZRIRBENTRY"></span> AzRirbEntry

```cpp
struct AzRirbEntry
{
  union
  {
    struct 
    {
      ULONG Response  : 21; // 0 : 20
      ULONG SubTag    : 5; // 21 : 25
      ULONG Tag       : 6; // 26 : 31
    } UnsolicitedForm;

    ULONG Response    : 32; // 0:31
  };
  ULONG Sdi         : 4;  // 32:35
  ULONG Unsolicited : 1;  // 36
  ULONG Reserved0   : 26; // 37:62
  ULONG Valid       : 1;  // 63 note this bit only exists
                          // on the "link". The fact that the response
                          // got into memory assures that it is valid
  AzRirbEntry (ULONGLONG x = 0)
  {
    Response = x & 0xffffffff;
    Sdi = x >> 32;
    Unsolicited = x >> 36;
    Reserved0 = x >> 37;
    Valid = x >> 63;
  }
  operator ULONGLONG()
  {
    return (ULONGLONG)Response | (ULONGLONG)Sdi << 32 | (ULONGLONG)Unsolicited << 36 | (ULONGLONG)Reserved0 << 37 | (ULONGLONG)Valid << 63;
  }
};
```

以下两个结构一起谓词传输 IOCTL，用于启用该命令和音频驱动程序和 HD 音频编解码器之间传输响应。

### <a name="span-idusermodecodeccommandpacketspanspan-idusermodecodeccommandpacketspan-usermodecodeccommandpacket"></a><span id="usermodecodeccommandpacket"></span><span id="USERMODECODECCOMMANDPACKET"></span> UserModeCodecCommandPacket

```cpp
typedef struct _UserModeCodecCommandPacket
{
  ULONG NumCommands;      // number of commands in this packet
  AzCorbEntry Command[1]; // variable length array of verbs
} UserModeCodecCommandPacket;
```

### <a name="span-idusermodecodecresponsepacketspanspan-idusermodecodecresponsepacketspan-usermodecodecresponsepacket"></a><span id="usermodecodecresponsepacket"></span><span id="USERMODECODECRESPONSEPACKET"></span> UserModeCodecResponsePacket

```cpp
typedef struct _UserModeCodecResponsePacket
{
  ULONG NumResponses;       // on successful IOCTL, this will be updated with the number of responses.
  AzRirbEntry Response[1];  // Variable length array of responses. lpOutBuffer param to DeviceIoControl
                            // must point to sufficient space to hold this IOCTL with all its responses 
} UserModeCodecResponsePacket;
```

 

 




