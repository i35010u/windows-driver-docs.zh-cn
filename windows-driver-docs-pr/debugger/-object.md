---
title: 对象
description: 对象扩展显示有关系统对象的信息。
ms.assetid: dc6d862b-3246-4d5b-992c-8723a0347f1d
keywords:
- Windows 调试对象
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- object
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3283e0d3d6c6bcec07896d8943ca1e9b19974808
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56564710"
---
# <a name="object"></a>!object


**！ 对象**扩展显示有关系统对象的信息。

```dbgcmd
!object Address [Flags] 
!object Path
!object 0 Name 
!object -p
!object {-h|-?}
```

## <a name="span-idddkobjectdbgspanspan-idddkobjectdbgspanparameters"></a><span id="ddk__object_dbg"></span><span id="DDK__OBJECT_DBG"></span>参数


<span id="_______Address______"></span><span id="_______address______"></span><span id="_______ADDRESS______"></span> *Address*   
如果第一个参数为非零值的十六进制数，它指定要显示的系统对象的十六进制地址。

<span id="_______Flags______"></span><span id="_______flags______"></span><span id="_______FLAGS______"></span> *标志*   
在命令输出中指定详细信息的级别。

设置*标志*到这些值的按位 OR:

<span id="0x0"></span><span id="0X0"></span>**0x0**  
显示对象类型。

<span id="0x1"></span><span id="0X1"></span>**0x1**  
显示对象类型、 对象名称和引用计数。

<span id="0x8"></span><span id="0X8"></span>**0x8**  
显示对象目录的内容或符号链接的目标。 此标志的效果才**0x1**还设置。

<span id="0x10"></span><span id="0X10"></span>**0x10**  
显示的可选对象标头。

<span id="0x20"></span><span id="0X20"></span>**0x20**  
向命名的对象显示的完整路径。 此标志的效果才**0x1**还设置。

*标志*参数是可选的。 默认值为 0x9。

<span id="_______Path______"></span><span id="_______path______"></span><span id="_______PATH______"></span> *路径*   
如果第一个参数以开始使用反斜杠 (\)， **！ 对象**将其解释为对象路径名称。 使用此选项时，将按照对象管理器所使用的目录结构排列显示。

<span id="_______Name______"></span><span id="_______name______"></span><span id="_______NAME______"></span> *名称*   
如果第一个参数为零，第二个参数被解释为要为其显示所有实例的系统对象的类的名称。

<span id="_______-p"></span><span id="_______-P"></span> **-p**  
显示私有对象的命名空间。

<span id="-h-_"></span><span id="-H-_"></span>{**-h**|**-?**}  
显示此命令的帮助。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

Kdexts.dll

### <a name="span-idexamplesspanspan-idexamplesspanspan-idexamplesspanexamples"></a><span id="Examples"></span><span id="examples"></span><span id="EXAMPLES"></span>示例

此示例将传递的路径\\设备目录更改为 **！ 对象**。 输出会列出中的所有对象\\设备目录。

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

选择一个列出的对象，假设 USBPDO 8。 将 USBPDO 8 (ffffe0083b85d060) 的地址传递给 **！ 对象**t。 设置*标志*为 0x0，若要获取的最少信息。

```dbgcmd
0: kd> !object ffffe0083b85d060 0x0
Object: ffffe0083b85d060  Type: (ffffe0083b87df20) Device
    ObjectHeader: ffffe0083b85d030 (new version)
```

通过设置包括相同的对象的名称和引用计数信息*标志*为 0x1。

```dbgcmd
0: kd> !object ffffe0083b85d060 0x1
Object: ffffe0083b85d060  Type: (ffffe0083b87df20) Device
    ObjectHeader: ffffe0083b85d030 (new version)
    HandleCount: 0  PointerCount: 6
    Directory Object: ffffc00b074166a0  Name: USBPDO-8
```

通过设置来获取相同的对象的可选标头信息*标志*到 0x10。

```dbgcmd
0: kd> !object ffffe0083b85d060 0x10
Object: ffffe0083b85d060  Type: (ffffe0083b87df20) Device
    ObjectHeader: ffffe0083b85d030 (new version)
Optional Headers: 
    NameInfo(ffffe0083b85d010)
```

下面的示例调用 **！ 对象**目录对象的两次。 第一次，目录的内容不会显示，因为未设置 0x8 标志。 第二次目录的内容显示因为 0x8 和 0x1 标志被设置 (标志 = 0x9)。

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

下面的示例调用 **！ 对象**两次以 SymbolicLink 对象。 第一次，因为未设置 0x8 标志，符号链接的目标不显示。 第二次，因为 0x8 和 0x1 标志被设置符号链接的目标 splayed (标志 = 0x9)。

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

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

有关对象和对象管理器的信息，请参阅 Microsoft Windows SDK 文档，Windows Driver Kit (WDK) 文档，并*Microsoft Windows Internals*、 Mark Russinovich 和 David solomon 合著的。

## <a name="span-idseealsospansee-also"></a><span id="see_also"></span>另请参阅


[对象引用跟踪](object-reference-tracing.md)

[**!obtrace**](-obtrace.md)

[**!handle**](-handle.md)

[确定对象的 ACL](determining-the-acl-of-an-object.md)

[内核模式扩展命令](kernel-mode-extensions.md)

 

 






