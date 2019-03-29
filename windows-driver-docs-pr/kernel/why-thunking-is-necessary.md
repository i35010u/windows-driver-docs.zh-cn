---
title: 为何需要进行形实转换
description: 为何需要进行形实转换
ms.assetid: ea73d355-56e8-4f56-b7e8-4dbddcd19124
keywords:
- 形式转换 WDK
- WOW64 形式转换层 WDK
- 32 位 I/O 支持 WDK 64 位形式转换
- 缓冲区大小 WDK 内核
- DRIVER_DATA 结构
- 指针精确度 WDK 64 位
- 固定精度数据类型 WDK 64 位
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0633f28cd2a8a9e6de09c5040a9e83011d51ecb8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564869"
---
# <a name="why-thunking-is-necessary"></a>为何需要进行形实转换





内核模式驱动程序必须验证任何传入从用户模式应用程序的 I/O 缓冲区的大小。 如果 32 位应用程序通过包含 64 位驱动程序，并没有形式转换为指针精度数据类型的缓冲区发生，该驱动程序将预期要比它实际上是更大的缓冲区。 这是因为指针精确度为 32 位上 32 位 Microsoft Windows 和 64 位 Windows 上的 64 位。 例如，考虑以下结构定义：

```cpp
typedef struct _DRIVER_DATA
{
    HANDLE           Event;
    UNICODE_STRING   ObjectName;
} DRIVER_DATA;
```

在 32 位 Windows，驱动程序的大小\_数据结构为 12 个字节。

处理**事件**UNICODE\_字符串**ObjectName** USHORT 长度 USHORT 最大长度 PWSTR 缓冲区 32 位 （4 字节） 16 位 （2 个字节） 16 位 （2 个字节） 32 位 （4 字节）
 

在 64 位 Windows，驱动程序的大小\_数据结构是 24 个字节。 (4 个字节的结构填充所需，以便**缓冲区**成员可以在一个 8 字节边界上对齐。)

处理**事件**UNICODE\_字符串**ObjectName** USHORT 长度 USHORT 最大长度为空 （结构填充） PWSTR 缓冲区 64 位 （8 个字节） 16 位 （2 个字节） 16 位 （2 个字节） 32 位 （4 字节）64 位 （8 个字节）
 

如果 64 位驱动程序收到 12 个字节的驱动程序\_数据时预期 24 个字节，大小验证将失败。 若要防止此情况，该驱动程序必须检测是否驱动程序\_数据结构已发送由 32 位应用程序，且如果是这样，thunk 其适当地执行验证之前。

例如，更高版本的驱动程序的 thunked 的版本\_可能按如下所示定义数据结构：

```cpp
typedef struct _DRIVER_DATA32
{
    VOID *POINTER_32   Event;
    UNICODE_STRING32   ObjectName;
} DRIVER_DATA32;
```

因为它仅包含固定精度的数据类型，此新的结构是 32 位 Windows 和 64 位 Windows 上的相同大小。

指针\_32**事件**UNICODE\_STRING32 **ObjectName** USHORT 长度 USHORT 最大长度 ULONG 缓冲区 32 位 （4 字节） 16 位 （2 个字节） 16 位 （2 个字节） 32 位 （4 字节）
 

 

 




