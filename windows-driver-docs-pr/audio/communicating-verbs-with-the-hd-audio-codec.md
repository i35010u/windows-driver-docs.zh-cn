---
title: 将谓词与 HD 音频编解码器通信
description: 将谓词与 HD 音频编解码器通信
ms.assetid: d93013fa-5b09-4616-bc71-5d3838337717
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 92d870d75a5aaa1400b8b3c7ac75781abe79d4c0
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90714816"
---
# <a name="communicating-verbs-with-the-hd-audio-codec"></a>将谓词与 HD 音频编解码器通信


\_ \_ 当你为音频适配器定义声音拓扑时，Hdau.exe 固定配置工具将使用 ioctl AZALIABUS SENDVERBS ioctl。 请勿将此 IOCTL 用于其他目的。 提供有关 IOCTL AZALIABUS SENDVERBS 的此信息 \_ \_ 以记录其设计和实现。 Windows 7 Hdaudio.sys 音频类驱动程序支持此 IOCTL。

高清晰度 (HD) 音频编解码器能够接收和响应动词。 这些动词和这些动词的编解码器的响应记录为 [高清音频规范](https://www.intel.com/content/www/us/en/products/docs/chipsets/high-definition-audio.html)的一部分。

在 windows 7 和更高版本的 Windows 操作系统中，HD audio 类驱动程序使用 IOCTL \_ AZALIABUS \_ SENDVERBS ioctl 与音频编解码器通信。 定义了 IOCTL \_ AZALIABUS \_ SENDVERBS，如以下示例中所示：

```cpp
#define IOCTL_AZALIABUS_SENDVERBS CTL_CODE(FILE_DEVICE_UNKNOWN, 1, METHOD_BUFFERED, FILE_ANY_ACCESS)
```

有关文件 \_ 设备 \_ 未知、 \_ 缓存方法和文件任何访问的详细 \_ 信息 \_ ，请参阅 Windows SDK 中的 Devioctl 标头文件。

若要启动与音频编解码器的通信，类驱动程序需要调用具有以下参数的 [DeviceIoControl](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 函数。

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

如果对 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) 的调用成功，它将返回一个非零值。 如果调用失败或挂起 (未立即处理) ，则 **DeviceIoControl** 将返回一个零值。 类驱动程序可以调用 [GetLastError](/windows/win32/api/errhandlingapi/nf-errhandlingapi-getlasterror) 以获取更详细的错误消息。

当音频驱动程序必须更改 pin 配置默认值时，它可以使用 IOCTL \_ AZALIABUS \_ SENDVERBS 来发送和接收设置，并从音频编解码器获取动词。 如果与音频编解码器的通信与 pin 配置无关，则音频编解码器仅响应 Get 谓词。

下面的示例演示一个函数，该函数采用 AzCorbeEntry 结构和句柄作为参数，并从编解码器返回 AzRirbResponse。

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

在下面的示例中定义了前面的代码示例中使用的数据类型和结构：

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

以下两个结构与动词传输 IOCTL 一起使用，以便在音频驱动程序和 HD 音频编解码器之间启用命令和响应传输。

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

 

