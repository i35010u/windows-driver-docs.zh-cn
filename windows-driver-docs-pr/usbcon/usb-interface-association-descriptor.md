---
Description: USB 接口关联描述符 (IAD) 允许设备连接到属于函数的组接口。
title: USB 接口关联描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1972b9b5a47db4d38c6feb0032bcfa8dab087af8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350722"
---
# <a name="usb-interface-association-descriptor"></a>USB 接口关联描述符


USB 接口关联描述符 (IAD) 允许设备连接到属于函数的组接口。 本主题介绍客户端驱动程序可以确定设备是否包含一个函数 IAD。

通用串行总线规范，修订版本 2.0 中，不支持对多个接口的一个函数内的复合设备进行分组。 但是，USB 设备使用组 (DWG) 创建 USB 设备类，使具有多个接口的函数和 USB 实现器的论坛发出定义分组接口的一种机制工程更改通知 (ECN)。

ECN 指定名为接口关联描述符 (IAD)，它允许硬件制造商定义的接口分组的 USB 描述符。 最有可能使用下列设备类包括：

-   USB 视频类规范 （类代码-0x0E）

-   USB 音频类规范 （类代码-0x01）

-   USB 蓝牙类规范 （类代码-0xE0）

Windows 7、 Windows Server 2008、 Windows Vista、 Microsoft Windows Server 2003 Service Pack 1 (SP1) 和 Microsoft Windows XP Service Pack 2 (SP2) 支持 Iad。

以下各小节介绍有关如何使用下列信息。

### <a href="" id="how-should-a-composite-device-alert-the-operating-system-that-it-has-i"></a>如何应复合设备警报操作系统它在其固件中具有 Iad？

复合设备制造商通常将分配到的设备类的零值 (*bDeviceClass*)，子类 (*bDeviceSubClass*)，和协议 (*bDeviceProtocol*) 的设备描述符，指定的通用串行总线规范中的字段。 这样，制造商联系，以将每个单独的接口与不同的设备类和协议相关联。

U-如果核心团队设计了特殊的类和协议代码集，通知操作系统的一个或多个 Iad 都位于设备固件。 设备的设备描述符必须具有下表中显示的值，否则操作系统将检测设备的 Iad 或正确组合设备的接口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>设备描述符字段</th>
<th>所需的值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>bDeviceClass</em></p></td>
<td><p>0xEF</p></td>
</tr>
<tr class="even">
<td><p><em>bDeviceSubClass</em></p></td>
<td><p>0x02</p></td>
</tr>
<tr class="odd">
<td><p><em>bDeviceProtocol</em></p></td>
<td><p>0x01</p></td>
</tr>
</tbody>
</table>

 

这些代码值提醒的 Windows 不支持下列安装正确枚举设备的特殊用途总线驱动程序的版本。 而无需设备描述符中的这些代码，系统可能无法枚举该设备，或者设备可能无法正常工作。

设备可具有多个 IAD。 每个 IAD 必须位于之前 IAD 描述的接口组中的接口。

函数类 (*bFunctionClass*)，子类 (*bFunctionSubclassClass*)，和协议 (*bFunctionProtocol*) IAD 字段必须包含的值指定的 USB 设备类描述在函数中的接口。

IAD 的类和子类字段不需要与 IAD 描述的接口集合中的接口的类和子类字段匹配。 但是，Microsoft 建议的集合的第一个接口具有与 IAD 的事件类和子类字段匹配的类和子类字段。 下表指示哪些字段应匹配。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>IAD 字段</th>
<th>相应的界面字段</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>bFunctionClass</em></p></td>
<td><p><em>bInterfaceClass</em></p></td>
</tr>
<tr class="even">
<td><p><em>bFunctionSubclassClass</em></p></td>
<td><p><em>bInterfaceSubClass</em></p></td>
</tr>
</tbody>
</table>

 

*BFirstInterface* IAD 字段指示的函数中的第一个接口。 *BInterfaceCount* IAD 字段指示接口集合中有多少个接口。 必须是连续的 IAD 接口集合中的接口 （可以有接口号码列表中的无间隔），因此，与第一个接口数字计数是不足以在集合中指定的所有接口。

### <a name="accessing-the-contents-of-an-iad"></a>访问 IAD 内容

客户端驱动程序不能直接访问 IAD 描述符。 IAD 工程更改通知 (ECN) 指定必须在设备返回一个请求收到配置描述符 （GetDescriptor 配置） 的主机软件时的配置信息中包含下列。 主机软件不能直接与 GetDescriptor 请求检索 Iad。

但是，客户端驱动程序可以查询设备的硬件标识符 (Id) 的 USB 设备的父驱动程序和设备的硬件 Id 包含嵌入的字段的 IAD 的信息。

### <a name="usb-interface-association-descriptor-example"></a>USB 接口关联描述符示例

以下说明了复合的 USB 设备的描述符布局。 示例设备有两种功能：

<a href="" id="function-1--video-class"></a>**函数 1:视频类**  
此函数由接口关联描述符 (IAD) 定义，并且包含两个接口： 零 (0) 和接口一 （1） 的接口。

系统生成的硬件和兼容标识符 (Id) 对于函数，如中所述[支持无线移动通信设备类](support-for-the-wireless-mobile-communication-device-class--wmcdc-.md)。 匹配相应的 INF 文件之后, 在系统加载视频类驱动程序堆栈。

<a href="" id="function-2--human-input-device"></a>**函数 2:人工输入的设备**  
该函数包含只有一个接口： 接口两 （2）。

系统生成的硬件和兼容 Id 对于函数，如中所述[枚举的接口集合 USB 复合设备上](support-for-interface-collections.md)。 匹配相应的 INF 文件之后, 在系统加载人工输入设备 (HID) 类驱动程序。

描述符如下所示：

### <a name="device-descriptor"></a>设备描述符：

```cpp
    BYTE  bLength      0x12
    BYTE  bDescriptorType    0x01
    WORD  bcdUSB      0x0200
    BYTE  bDeviceClass     0xEF
    BYTE  bDeviceSubClass   0x02
    BYTE  bDeviceProtocol    0x01
    BYTE  bMaxPacketSize0   0x40
    WORD  idVendor      0x045E
    WORD  idProduct      0xFFFF
    WORD  bcdDevice     0x0100
    BYTE  iManufacturer     0x01
    WORD  iProduct      0x02
    WORD  iSerialNumber    0x02
    BYTE  bNumConfigurations  0x01
```

### <a name="configuration-descriptor"></a>配置描述符：

```cpp
    BYTE  bLength      0x09
    BYTE  bDescriptorType    0x02
    WORD  wTotalLength    0x....
    BYTE  bNumInterfaces    0x03
    BYTE  bConfigurationValue  0x01
    BYTE  iConfiguration     0x01
    BYTE  bmAttributes     0x80 (BUS Powered)
    BYTE  bMaxPower     0x19 (50 mA)
```

### <a name="interface-association-descriptor"></a>接口关联描述符：

```cpp
    BYTE  bLength      0x08
    BYTE  bDescriptorType    0x0B
    BYTE  bFirstInterface    0x00
    BYTE  bInterfaceCount    0x02
    BYTE  bFunctionClass    0x0E
    BYTE  bFunctionSubClass   0x03
    BYTE  bFunctionProtocol   0x00
    BYTE  iFunction      0x04
```

### <a name="interface-descriptor-video-control"></a>接口描述符 （视频控件）：

```cpp
    BYTE  bLength      0x09
    BYTE  bDescriptorType    0x04
    BYTE  bInterfaceNumber   0x00
    BYTE  bAlternateSetting   0x00
    BYTE  bNumEndpoints    0x01
    BYTE  bInterfaceClass    0x0E
    BYTE  bInterfaceSubClass   0x01
    BYTE  bInterfaceProtocol   0x00
    BYTE  iInterface      0x05
```

### <a name="class-specific-descriptors"></a>类特定 Descriptor(s):

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a name="endpoint-descriptors"></a>终结点 Descriptor(s):

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a name="interface-descriptor-video-streaming"></a>接口 （视频流式处理） 的描述符：

```cpp
    BYTE  bLength      0x09
    BYTE  bDescriptorType    0x04
    BYTE  bInterfaceNumber   0x01
    BYTE  bAlternateSetting   0x00
    BYTE  bNumEndpoints    0x01
    BYTE  bInterfaceClass    0x0E
    BYTE  bInterfaceSubClass   0x02
    BYTE  bInterfaceProtocol   0x00
    BYTE  iInterface      0x06
```

### <a href="" id="class-specific-descriptor-s--video"></a>类特定 Descriptor(s):

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a href="" id="endpoint-descriptor-s--video"></a>终结点 Descriptor(s):

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a name="interface-descriptor-human-input-devices"></a>接口描述符 （人工输入设备）：

```cpp
    BYTE  bLength      0x09
    BYTE  bDescriptorType    0x04
    BYTE  bInterfaceNumber   0x02
    BYTE  bAlternateSetting   0x00
    BYTE  bNumEndpoints    0x01
    BYTE  bInterfaceClass    0x03
    BYTE  bInterfaceSubClass   0x01
    BYTE  bInterfaceProtocol   0x01
    BYTE  iInterface      0x07
```

### <a href="" id="class-specific-descriptor-s--hid"></a>类特定 Descriptor(s):

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a href="" id="endpoint-descriptor-s--hid"></a>终结点 Descriptor(s):

``` syntax
    . . . .
    . . . .
    . . . .
```

## <a name="related-topics"></a>相关主题
[USB 描述符](usb-descriptors.md)  



