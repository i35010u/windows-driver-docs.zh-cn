---
title: 对象
description: 对象扩展显示有关系统对象的信息。
keywords:
- 对象 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- object
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f1081f0442660feeb9018c5e6c1c4eb6feabb8c9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795227"
---
# <a name="object"></a>!object


**！对象** 扩展显示有关系统对象的信息。

```dbgcmd
!object Address [Flags] 
!object Path
!object 0 Name 
!object -p
!object {-h|-?}
```

## <a name="span-idddk__object_dbgspanspan-idddk__object_dbgspanparameters"></a><span id="ddk__object_dbg"></span><span id="DDK__OBJECT_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span>*地址*   
如果第一个参数为非零十六进制数字，则它指定要显示的系统对象的十六进制地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span>*标志*   
指定命令输出中的详细信息级别。

将 *标志* 设置为这些值的按位 "或"：

<span id="0x0"></span><span id="0X0"></span>**0x0**  
显示对象类型。

<span id="0x1"></span><span id="0X1"></span>**0x1**  
显示对象类型、对象名称和引用计数。

<span id="0x8"></span><span id="0X8"></span>**0x8**  
显示对象目录或符号链接的目标的内容。 仅当同时设置了 **0x1** 时，此标志才有效。

<span id="0x10"></span><span id="0X10"></span>**0x10**  
显示可选对象标头。

<span id="0x20"></span><span id="0X20"></span>**0x20**  
显示指定对象的完整路径。 仅当同时设置了 **0x1** 时，此标志才有效。

*Flags* 参数是可选的。 默认值为0x9。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span>*路径*   
如果第一个参数以反斜杠开头 (\) ， **！对象** 会将其解释为对象路径名称。 使用此选项时，将根据对象管理器使用的目录结构排列显示。

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span>*名称*   
如果第一个参数为零，则第二个参数被解释为要显示其所有实例的系统对象类的名称。

<span id="_______-p"></span><span id="_______-P"></span>**-p**  
显示专用对象命名空间。

<span id="-h-_"></span><span id="-H-_"></span>{**-h** |**-?**}  
显示此命令的帮助。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Kdexts.dll

### <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例

此示例将设备目录的路径传递 \\ 给 **！对象**。 输出会列出设备目录中的所有对象 \\ 。

```dbgcmd
0: kd> !object \Device
Object: ffffc00b074166a0  Type: (ffffe0083b768690) Directory
    ObjectHeader: ffffc00b07416670 (new version)
    HandleCount: 0  PointerCount: 224
    Directory Object: ffffc00b074092e0  Name: Device

    Hash Address          Type          Name
    ---- -------          ----          ----
     00  ffffe0083e6a61f0 Device        00000044
         ffffe0083dcc4050 Device        00000030
         ffffe0083d34f050 Device        NDMP2
         ffffe0083bdf7060 Device        NTPNP_PCI0002
         ...
         ffffe0083b85d060 Device        USBPDO-8
         ffffe0083d33d050 Device        USBFDO-6
         ...
         ffffe0083bdf0060 Device        NTPNP_PCI0001
```

选择列出的对象之一，如 USBPDO-8。 将 USBPDO (ffffe0083b85d060) 的地址传递给 **！对象传递** t。 将 *标志* 设置为0x0 以获取最少信息。

```dbgcmd
0: kd> !object ffffe0083b85d060 0x0
Object: ffffe0083b85d060  Type: (ffffe0083b87df20) Device
    ObjectHeader: ffffe0083b85d030 (new version)
```

通过将 *标志* 设置为0x1，为同一对象包含名称和引用计数信息。

```dbgcmd
0: kd> !object ffffe0083b85d060 0x1
Object: ffffe0083b85d060  Type: (ffffe0083b87df20) Device
    ObjectHeader: ffffe0083b85d030 (new version)
    HandleCount: 0  PointerCount: 6
    Directory Object: ffffc00b074166a0  Name: USBPDO-8
```

通过将 *标志* 设置为0x10，为同一对象获取可选的标头信息。

```dbgcmd
0: kd> !object ffffe0083b85d060 0x10
Object: ffffe0083b85d060  Type: (ffffe0083b87df20) Device
    ObjectHeader: ffffe0083b85d030 (new version)
Optional Headers: 
    NameInfo(ffffe0083b85d010)
```

下面的示例调用一个目录对象的两个 **对象** 。 第一次时，不会显示该目录的内容，因为未设置0x8 标志。 第二次将显示目录的内容，因为0x8 和0x1 标志都设置 (Flags = 0x9) 。

```dbgcmd
0: kd> !object ffffc00b07481d00 0x1
Object: ffffc00b07481d00  Type: (ffffe0083b768690) Directory
    ObjectHeader: ffffc00b07481cd0 (new version)
    HandleCount: 0  PointerCount: 3
    Directory Object: ffffc00b07481eb0  Name: Filters

0: kd> !object ffffc00b07481d00 0x9
Object: ffffc00b07481d00  Type: (ffffe0083b768690) Directory
    ObjectHeader: ffffc00b07481cd0 (new version)
    HandleCount: 0  PointerCount: 3
    Directory Object: ffffc00b07481eb0  Name: Filters

    Hash Address          Type          Name
    ---- -------          ----          ----
     19  ffffe0083c5f56e0 Device        FltMgrMsg
     21  ffffe0083c5f5060 Device        FltMgr
```

下面的示例调用一个 SymbolicLink 对象的两个 **对象** 。 第一次，将不会显示符号链接的目标，因为未设置0x8 标志。 第二次，符号链接的目标为的，因为在 Flags 和0x1 标志 (都设置为 Flags = 0x9) 。

```dbgcmd
0: kd> !object ffffc00b07628fb0 0x1
Object: ffffc00b07628fb0  Type: (ffffe0083b769450) SymbolicLink
    ObjectHeader: ffffc00b07628f80 (new version)
    HandleCount: 0  PointerCount: 1
    Directory Object: ffffc00b074166a0  Name: Ip6

0: kd> !object ffffc00b07628fb0 0x9
Object: ffffc00b07628fb0  Type: (ffffe0083b769450) SymbolicLink
    ObjectHeader: ffffc00b07628f80 (new version)
    HandleCount: 0  PointerCount: 1
    Directory Object: ffffc00b074166a0  Name: Ip6
    Target String is '\Device\Tdx'
```

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关对象和对象管理器的信息，请参阅 Microsoft Windows SDK 文档、Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部*，并将其标记为 Russinovich 和 David 所罗门群岛。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[对象引用跟踪](object-reference-tracing.md)

[**!obtrace**](-obtrace.md)

[**!handle**](-handle.md)

[确定对象的 ACL](determining-the-acl-of-an-object.md)

[内核模式扩展命令](kernel-mode-extensions.md)

 

 






