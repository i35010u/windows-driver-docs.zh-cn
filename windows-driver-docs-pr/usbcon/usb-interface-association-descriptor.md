---
description: USB 接口关联描述符 (IAD) 允许设备对属于某个函数的接口进行分组。
title: USB 接口关联描述符
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9679d0ae156a19cace11ba3450a408508b52b28d
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90010027"
---
# <a name="usb-interface-association-descriptor"></a>USB 接口关联描述符


USB 接口关联描述符 (IAD) 允许设备对属于某个函数的接口进行分组。 本主题介绍客户端驱动程序如何确定设备是否包含用于函数的 IAD。

通用串行总线规范版本2.0 不支持将复合设备的多个接口分组到一个函数中。 但是，USB 设备工作组 (DWG) 创建了允许使用多个接口的功能的 USB 设备类，而 USB 实现器的论坛发出了一个工程更改通知 (ECN) ，定义了用于分组接口的机制。

ECN 指定一个 USB 描述符（称为接口关联描述符 (IAD) ），该描述符允许硬件制造商定义接口分组。 最有可能使用 IADs 的设备类包括：

-   USB 视频类规范 (类代码-0x0E) 

-   USB 音频类规范 (类代码-0x01) 

-   USB 蓝牙类规范 (类代码-0xE0) 

Windows 7、Windows Server 2008、Windows Vista、Microsoft Windows Server 2003 Service Pack 1 (SP1) 和 Microsoft Windows XP Service Pack 2 (SP2) 支持 IADs。

以下小节介绍有关如何使用 IADs 的信息。

### <a name="how-should-a-composite-device-alert-the-operating-system-that-it-has-iads-in-its-firmware"></a><a href="" id="how-should-a-composite-device-alert-the-operating-system-that-it-has-i"></a>复合设备应该如何向操作系统提醒其固件中已 IADs？

复合设备制造商通常会将零值分配给设备类 (*bDeviceClass*) 、子类 (*bDeviceSubClass*) 和协议 (*BDeviceProtocol* ，这是由通用串行总线规范指定的设备描述符中) 字段。 这允许制造商将各个接口与不同的设备类和协议相关联。

USB 假设核心团队已经设计了一个特殊的类和协议代码集，用于通知操作系统一个或多个 IADs 存在于设备固件中。 设备的设备描述符必须具有下表中显示的值，否则，操作系统将不会检测到设备的 IADs，也不会正确地对设备的接口进行分组。

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

 

这些代码值还提醒 Windows 版本，这些版本不支持 IADs 来安装正确枚举设备的专用总线驱动程序。 如果设备描述符中没有这些代码，系统可能无法枚举设备，或者设备可能无法正常工作。

一个设备可以有多个 IAD。 每个 IAD 必须紧跟在 IAD 所描述的接口组中的接口之前。

函数类 (*bFunctionClass*) 、子类 (*bFunctionSubclassClass*) 和协议 (BFUNCTIONPROTOCOL) 字段。 IAD 的*bFunctionProtocol*字段必须包含由描述函数中的接口的 USB 设备类指定的值。

IAD 的 "类" 和 "子类" 字段不需要匹配 IAD 所描述的接口集合中接口的 "类" 和 "子类" 字段。 但是，Microsoft 建议集合的第一个接口具有与 IAD 的 "类" 和 "子类" 字段匹配的 "类" 和 "子类" 字段。 下表指示哪些字段应该匹配。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>IAD 字段</th>
<th>对应的接口字段</th>
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

 

IAD 的 *bFirstInterface* 字段指示函数中第一个接口的编号。 IAD 的 *bInterfaceCount* 字段指示接口集合中有多少个接口。 IAD 接口集合中的接口必须是连续的 (在) 的接口号列表中不能有间隔，因此具有第一个接口号的计数足以指定集合中的所有接口。

### <a name="accessing-the-contents-of-an-iad"></a>访问 IAD 的内容

客户端驱动程序无法直接访问 IAD 描述符。 IAD 工程更改通知 (ECN) 指定 IADs 必须包括在设备接收来自主机软件的请求时返回的配置信息， (GetDescriptor Configuration) 。 主机软件无法直接使用 GetDescriptor 请求检索 IADs。

但是，客户端驱动程序可以在 USB 设备的父驱动程序中查询设备的硬件标识符 (Id) ，设备的硬件 Id 包含有关 IAD 字段的嵌入信息。

### <a name="usb-interface-association-descriptor-example"></a>USB 接口关联描述符示例

下面演示了复合 USB 设备的描述符布局。 该示例设备有两个功能：

<a href="" id="function-1--video-class"></a>**函数1： Video 类**  
此函数由接口关联描述符 (IAD) 定义，其中包含两个接口： interface 0 (0) 和 interface one (1) 。

系统将为函数)  (Id 生成硬件和兼容标识符，如对 [无线移动通信设备类的支持](./support-for-interface-collections.md)中所述。 匹配适当的 INF 文件后，系统会加载视频类驱动程序堆栈。

<a href="" id="function-2--human-input-device"></a>**函数2：人体输入设备**  
此函数只包含一个接口： interface 2 (2) 。

系统会为该函数生成硬件和兼容 Id，如 [USB 复合设备上的接口集合枚举](support-for-interface-collections.md)中所述。 匹配适当的 INF 文件后，系统会 (HID) 类驱动程序加载人体输入设备。

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

### <a name="interface-descriptor-video-control"></a>接口描述符 (视频控制) ：

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

### <a name="class-specific-descriptors"></a>)  (类特定描述符：

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a name="endpoint-descriptors"></a>终结点描述符 (s) ：

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a name="interface-descriptor-video-streaming"></a>接口描述符 (视频流式处理) ：

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

### <a name="class-specific-descriptors"></a><a href="" id="class-specific-descriptor-s--video"></a>)  (类特定描述符：

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a name="endpoint-descriptors"></a><a href="" id="endpoint-descriptor-s--video"></a>终结点描述符 (s) ：

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a name="interface-descriptor-human-input-devices"></a>)  (人输入设备的接口描述符：

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

### <a name="class-specific-descriptors"></a><a href="" id="class-specific-descriptor-s--hid"></a>)  (类特定描述符：

``` syntax
    . . . .
    . . . .
    . . . .
```

### <a name="endpoint-descriptors"></a><a href="" id="endpoint-descriptor-s--hid"></a>终结点描述符 (s) ：

``` syntax
    . . . .
    . . . .
    . . . .
```

## <a name="related-topics"></a>相关主题
[USB 描述符](usb-descriptors.md)