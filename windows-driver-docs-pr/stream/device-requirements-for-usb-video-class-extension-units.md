---
title: USB 视频类扩展单元的设备要求
description: USB 视频类扩展单元的设备要求
ms.assetid: 4678c3a4-9ca7-4518-afe8-99a9e61f3dcd
keywords:
- 扩展单位 WDK USB 视频类，设备要求
- 扩展单元描述符 WDK USB 视频类
- 描述符 WDK USB 视频类
- 扩展单元控制 WDK USB 视频类
- 控件 WDK USB 视频类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c680785262c524ba991a549096bf144e9102aea
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568962"
---
# <a name="device-requirements-for-usb-video-class-extension-units"></a>USB 视频类扩展单元的设备要求


本部分介绍一些特定的要求在设备中实现一个扩展单元。 如果不满足这些要求，USB 视频类驱动程序可能无法正常工作与扩展单元。

## <a name="descriptor"></a>描述符


扩展单元描述符必须包含有效的唯一 GUID。 此 GUID 是 Usbvideo.sys 用于公开相应的扩展节点上设置的属性。 通过使用名为 Guidgen.exe 使用 Microsoft Windows SDK 附带的工具，应为扩展单元创建的唯一 GUID。

扩展单元属性集的属性标识符 (KSPROPERTY\_扩展\_单元) 对应于同样带编号的扩展单元控件公开的 USB 视频类固件的 Id。 可以通过使用标准 KSPROPERTY 请求通过 IKsControl 界面访问扩展单元控件。

扩展单元，称为扩展单元控件 Id，控件必须为编号持续从 1 到一些最大值 n。 如果有间隙，USB 视频类驱动程序不公开控件包含同时位于超出了无缝连接。 USB 视频类驱动程序的当前实现限制到 31 之间的一个扩展单元上的控件数。

使用属性 ID = 0 (KSPROPERTY\_扩展\_单元\_信息) 若要获取的扩展单元描述符的一部分，其语法通过通用串行总线设备类定义视频设备规范定义。 此规范位于[USB 实现论坛](https://go.microsoft.com/fwlink/p/?linkid=8780)网站。

使用属性 ID = 1 和更高版本才能将请求发送到相应的扩展单元控件。

请注意该 KSPROPERTY\_扩展\_单元\_控件 (属性 ID = 1) 不是一个真正的属性。 相反，它表示 1 和更高版本的标识符引用实际扩展单元控件 Id。

KSPROPERTY\_扩展\_单元\_传递\_THROUGH (属性 ID = 0xffff) 未实现。

下面的代码示例中，来自完整示例扩展单元插件 DLL 中所示的示例演示如何使 KSPROPERTY\_扩展\_单元\_信息请求：

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


设备必须支持 GET\_CUR，获取\_信息，GET\_LEN、 GET\_最小值、 GET\_最大值，获取\_DEF，并获取\_RES 请求根据所有扩展单元控件USB 视频类规范。 如果你的设备不实现这些函数，为用户模式不会公开相应的属性。

设备在初始化期间，驱动程序向设备颁发以下控制请求：获取\_信息，GET\_LEN、 GET\_最小值和 GET\_最大值。 如果任何这些初始请求失败，Usbvideo.sys 禁用特定的控件。

获取返回的值\_信息指示驱动程序的 GET 和 SET 请求适用于在给定控件。 此外，获取\_信息指示驱动程序的控件是否异步。 中断状态的终结点支持的异步请求。

 

 




