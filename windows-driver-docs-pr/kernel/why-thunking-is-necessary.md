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
ms.openlocfilehash: 70536b398320156eda68efc2c002672052940253
ms.sourcegitcommit: a0e6830b125a86ac0a0da308d5bf0091e968b787
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86557740"
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

在32位 Windows 中，驱动程序 \_ 数据结构的大小为12个字节。 此表显示了 DRIVER_DATA 结构的**事件**成员和**ObjectName**成员的大小：

|事件|ObjectName （USHORT 长度）|ObjectName （USHORT 最大长度）|ObjectName （PWSTR Buffer）|
|----|----|----|---|
|32 位|16 位|16 位|32 位|
|（4字节）|（2个字节）|（2个字节）|（4字节）|

在64位 Windows 中，驱动程序 \_ 数据结构的大小为24个字节。 （需要4个字节的结构填充，以便可以在8字节边界上对齐**缓冲区**成员。）

|事件|ObjectName （USHORT 长度）|ObjectName （USHORT 最大长度）|空（结构填充）|ObjectName （PWSTR Buffer）|
|----|----|----|----|----|
|64 位|16 位|16 位|32 位|64 位|
|（8字节）|（2个字节）|（2个字节）|（4字节）|（8字节）|

如果64位驱动程序在需要24个字节时接收12个字节的驱动程序 \_ 数据，则大小验证将失败。 若要防止出现这种情况，驱动程序必须检测驱动程序 \_ 数据结构是否由32位应用程序发送，如果是，则在执行验证之前将其正确地转换。

例如，可以定义以上驱动程序数据结构的 thunked 版本， \_ 如下所示：

```cpp
typedef struct _DRIVER_DATA32
{
    VOID *POINTER_32   Event;
    UNICODE_STRING32   ObjectName;
} DRIVER_DATA32;
```

由于它只包含固定精度的数据类型，因此在32位 Windows 和64位 Windows 上，此新结构的大小相同。

|事件|ObjectName （USHORT 长度）|ObjectName （USHORT 最大长度）|ULONG 缓冲区|
|----|----|----|----|
|32 位|16 位|16 位|32 位|
|（4字节）|（2个字节）|（2个字节）|（4字节）|
