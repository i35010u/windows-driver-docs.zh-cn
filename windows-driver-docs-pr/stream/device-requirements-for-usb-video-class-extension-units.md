---
title: USB 视频类扩展单元的设备要求
description: USB 视频类扩展单元的设备要求
keywords:
- 扩展单元-WDK USB 视频类，设备要求
- 扩展单元描述符 WDK USB 视频类
- 描述符 WDK USB 视频类
- 扩展单元控制 WDK USB 视频类
- 控制 WDK USB 视频类
ms.date: 06/16/2020
ms.localizationpriority: medium
ms.openlocfilehash: 54bf13879a7eea979074853362e95b7ade9861b5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830881"
---
# <a name="device-requirements-for-usb-video-class-extension-units"></a>USB 视频类扩展单元的设备要求

本部分介绍在设备中实现扩展单元的一些具体要求。 如果未满足这些要求，则 USB 视频类驱动程序可能无法与扩展单元一起正常工作。

## <a name="descriptor"></a>描述符

扩展单元描述符必须包含有效的唯一 GUID。 此 GUID 由 Usbvideo.sys 用来公开在相应扩展节点上设置的属性。 应使用 Microsoft Windows SDK 附带的名为 Guidgen.exe 的工具创建扩展单元的唯一 GUID。

扩展单元属性集上的属性标识符 (KSPROPERTY \_ Extension \_ unit) 对应于 USB 视频类固件公开的编号相同的扩展单元控制 id。 可以通过 IKsControl 接口使用标准 KSPROPERTY 请求访问扩展单元控件。

扩展单元上的控件（称为扩展单元控件 Id）必须连续编号为1到一些最大值 n。 如果有空白，则 USB 视频类驱动程序不会公开超出该间隔的控件。 USB 视频类驱动程序的当前实现将扩展单元上的控件数限制为31。

使用属性 ID = 0 (KSPROPERTY \_ extension \_ unit \_ INFO) 以获取扩展单元描述符的一部分，它是由视频设备规范的通用串行总线设备类定义定义的语法。 此规范可在 [USB 实现论坛](https://www.usb.org/) 网站上找到。

使用属性 ID = 1 和更高版本将请求发送到相应的扩展单元控件。

请注意，KSPROPERTY \_ EXTENSION \_ UNIT \_ CONTROL (属性 ID = 1) 不是真实属性。 相反，它表示标识符1和更高版本引用实际扩展单元控件 Id。

KSPROPERTY \_ 扩展 \_ 单元 \_ 传递 \_ (属性 ID = 0xffff) 未实现。

下面的代码示例摘自示例扩展插件 DLL 中所示的完整示例，演示了如何发出 KSPROPERTY \_ 扩展 \_ 单元 \_ 信息请求：

```cpp
ExtensionProp.Property.Set = PROPSETID_VIDCAP_EXTENSION_UNIT;
    ExtensionProp.Property.Id = KSPROPERTY_EXTENSION_UNIT_INFO;
    ExtensionProp.Property.Flags = KSPROPERTY_TYPE_GET |
                                   KSPROPERTY_TYPE_TOPOLOGY;
    ExtensionProp.NodeId = m_dwNodeId;

    hr = m_pKsControl->KsProperty(
        (PKSPROPERTY) &ExtensionProp,
                  sizeof(ExtensionProp),
        (PVOID) pInfo,
        ulSize,
        &ulBytesReturned);

        return hr;
}
```

## <a name="control-requests"></a>控制请求

设备必须支持 "获取 \_ 当前"、"获取 \_ 信息"、"获取长度"、"获得 \_ \_ 最小值"、 \_ "获取最大值"、"获取 \_ 定义"，并 \_ 根据 USB 视频类规范为所有扩展单元控件获取 RES 请求。 如果设备未实现这些功能，则不会向用户模式公开相应的属性。

在设备初始化过程中，驱动程序向设备发出以下控制请求：获取 \_ 信息、获取 \_ 长度、获取 \_ 最小值和获取 \_ 最大值。 如果这些初始请求中有任何一个失败，Usbvideo.sys 会禁用特定控件。

"获取信息" 返回的值 \_ 告诉驱动程序： get 和 SET 请求对于给定的控件有效。 此外，"获取 \_ 信息" 会告诉驱动程序控件是否为异步控件。 状态中断终结点支持异步请求。
