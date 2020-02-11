---
title: 为何需要进行形实转换
description: 为何需要进行形实转换
ms.assetid: ea73d355-56e8-4f56-b7e8-4dbddcd19124
keywords:
- thunk WDK
- WOW64 thunk 层 WDK
- 32位 i/o 支持 WDK 64 位，thunk
- 缓冲区大小 WDK 内核
- DRIVER_DATA 结构
- 指针精度 WDK 64 位
- 固定精度数据类型 WDK 64 位
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37a2b47ddd1ed4bd94345fa7128cd518e6aa103c
ms.sourcegitcommit: f6aebb32c045b9da7da4bf9b3fd8d6fad05e9deb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/10/2020
ms.locfileid: "77114479"
---
# <a name="why-thunking-is-necessary"></a>为何需要进行形实转换

内核模式驱动程序必须验证从用户模式应用程序传入的任何 i/o 缓冲区的大小。 如果32位应用程序将包含指针精度数据类型的缓冲区传递到64位驱动程序，并且不会发生 thunk，则驱动程序将预期缓冲区比实际的要大。 这是因为在32位的 Microsoft Windows 上，指针精确度为32位，在64位 Windows 上为64位。 例如，请考虑以下结构定义：

```cpp
typedef struct _DRIVER_DATA
{
    HANDLE           Event;
    UNICODE_STRING   ObjectName;
} DRIVER_DATA;
```

在32位 Windows 上，\_数据结构的驱动程序大小为12个字节。

|处理事件|UNICODE\_字符串 ObjectName|||
|----|----|----|---|
||**USHORT 长度**|**USHORT 最大长度**|**PWSTR 缓冲区**|
|32位|16位|16位|32位|
|（4字节）|（2个字节）|（2个字节）|（4字节）|

在64位 Windows 中，驱动程序\_数据结构的大小为24个字节。 （需要4个字节的结构填充，以便可以在8字节边界上对齐**缓冲区**成员。）

|处理事件|UNICODE\_字符串 ObjectName||||
|----|----|----|----|----|
||**USHORT 长度**|**USHORT 最大长度**|**空（结构填充）**|**PWSTR 缓冲区**|
|64位|16位|16位|32位|64位|
|（8字节）|（2个字节）|（2个字节）|（4字节）|（8字节）|

如果64位驱动程序在需要24个字节时收到12个\_数据的驱动程序，则大小验证将失败。 若要防止出现这种情况，驱动程序必须检测32位应用程序是否发送了驱动程序\_数据结构，如果是，则在执行验证之前将其正确地转换。

例如，可以按如下所示定义以上驱动程序的 thunked 版本\_的数据结构：

```cpp
typedef struct _DRIVER_DATA32
{
    VOID *POINTER_32   Event;
    UNICODE_STRING32   ObjectName;
} DRIVER_DATA32;
```

由于它只包含固定精度的数据类型，因此在32位 Windows 和64位 Windows 上，此新结构的大小相同。

|指针\_32 事件|UNICODE\_STRING32 ObjectName|||
|----|----|----|----|
||**USHORT 长度**|**USHORT 最大长度**|**ULONG 缓冲区**|
|32位|16位|16位|32位|
|（4字节）|（2个字节）|（2个字节）|（4字节）|
