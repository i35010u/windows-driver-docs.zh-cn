---
title: JavaScript 调试器示例脚本
description: 本主题提供有关用户和内核模式 JavaScript 代码示例的信息，如数据筛选即插即用设备树示例。
ms.assetid: F477430B-10C7-4039-9C5F-25556C306643
ms.date: 02/27/2019
ms.localizationpriority: medium
ms.openlocfilehash: 096f60f375f7f8c71c3ae5b9d1afd4efdfa50003
ms.sourcegitcommit: f610410e1500f0b0a4ca008b52679688ab51033d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/15/2020
ms.locfileid: "88252915"
---
# <a name="javascript-debugger-example-scripts"></a>JavaScript 调试器示例脚本

本主题提供了以下用户和内核模式 JavaScript 代码示例。

- [确定进程体系结构](#processarchitecture)
- [数据筛选： KD (内核模式下即插即用设备树) ](#filter)
- [将特定于多媒体 (内核模式的设备扩展) ](#multimedia)
- [ (内核模式将总线信息添加到 \_ 设备 \_ 对象) ](#bus)
- [ (用户模式下查找应用程序标题) ](#title)

## <a name="microsoft-github-repo-example-scripts"></a>Microsoft GitHub 存储库示例脚本

调试器团队承载包含 JavaScript 脚本和扩展示例的 GitHub 存储库。

可以在- https://github.com/Microsoft/WinDbg-Samples

自述文件介绍了当前可用的示例代码。

## <a name="span-idworking_with_samplesspanspan-idworking_with_samplesspanspan-idworking_with_samplesspanworking-with-samples"></a><span id="Working_with_Samples"></span><span id="working_with_samples"></span><span id="WORKING_WITH_SAMPLES"></span>使用示例

使用常规过程来测试任何示例。

1. 确定示例 JavaScript 是否用于内核模式或用户模式调试。 然后加载相应的转储文件或建立与目标系统的实时连接。

2. 使用文本编辑器（如记事本）创建名为的文本文件，并使用 .js 文件扩展名保存该文件，例如 *HelloWorld.js*

```javascript
// WinDbg JavaScript sample
// Says Hello World!

// Code at root will be run with .scriptrun and .scriptload
host.diagnostics.debugLog("***> Hello World! \n");

function sayHi()
{
   //Say Hi 
   host.diagnostics.debugLog("Hi from JavaScript! \n");
}
```

3. 使用 [**load (负载扩展 DLL) **](-load---loadby--load-extension-dll-.md) 命令加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

4. 使用 [**scriptrun (运行脚本) **](-scriptrun--run-script-.md)命令加载和执行脚本。 Scriptrun 命令将在 root/top 和函数名称 *initializeScript* 和 *invokeScript*下运行代码。

```dbgcmd
0:000> .scriptrun c:\WinDbg\Scripts\HelloWorld.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\HelloWorld.js'
***> Hello World! 
```

5. 如果脚本包含唯一命名的函数，请使用 dx 命令执行该函数，该函数位于调试程序中。*ScriptName*。目录.*FunctionName*。

```dbgcmd
0:001> dx Debugger.State.Scripts.HelloWorld.Contents.sayHi()
Hi from JavaScript!
Debugger.State.Scripts.HelloWorld.Contents.sayHi()
```

有关使用 JavaScript 的其他信息，请参阅 [JavaScript 调试器脚本](javascript-debugger-scripting.md) 。

## <a name="span-idprocessarchitecturespanspan-idprocessarchitecturespanspan-idprocessarhcitecturespandetermining-process-architecture"></a><span id="Processarchitecture"></span><span id="processarchitecture"></span><span id="PROCESSARHCITECTURE"></span>确定进程体系结构

此 JavaScript 代码将在上向调试器对象模型进程对象添加一个名为 "ProcessArchitecture" 的属性，以指示该过程是 x86 还是 x64。

此脚本旨在支持内核模式调试。

```JavaScript
"use strict";

class __CheckArchitecture
{
//
// Add a property called 'ProcessArchitecture' on process.
//
    get ProcessArchitecture()
    {
    var guestStates = this.Threads.Any(t=> (!(t.GuestState === undefined) && t.GuestState.Architecture =="x86"));
 
        if(guestStates)
            return "x86";
        else
            return "x64";
    }
};
 
function initializeScript()
{
//
// Extends our notion of a process to place architecture information on it.
//
return [new host.namedModelParent(__CheckArchitecture, "Debugger.Models.Process")];
}
```

加载内核转储文件或建立与目标系统的内核模式连接。 然后加载 JavaScript 提供程序和示例脚本。

```dbgcmd
0: kd> !load jsprovider.dll
```

```dbgcmd
0: kd> .scriptload c:\WinDbg\Scripts\processarchitecture.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\processarchitecture.js'
```

使用 [dx](dx--display-visualizer-variables-.md) 命令显示当前进程的进程体系结构。

```dbgcmd
2: kd> dx @$curprocess
@$curprocess                 : System [Switch To]
    KernelObject     [Type: _EPROCESS]
    Name             : System
    Id               : 0x4
    Handle           : 0xf0f0f0f0
    Threads         
    Modules         
    Environment     
    Devices         
    Io              
    ProcessArchitecture : x64
```

请注意，此示例代码可能并不总是能够正确确定体系结构。 例如，在某些情况下，使用32位调试器时使用转储文件。

## <a name="span-idfilterspanspan-idfilterspanspan-idfilterspandata-filtering-plug-and-play-device-tree-in-kd-kernel-mode"></a><span id="Filter"></span><span id="filter"></span><span id="FILTER"></span>数据筛选： KD (内核模式下即插即用设备树) 

此示例代码筛选设备节点树，只显示包含已启动的 PCI 路径的设备。

此脚本旨在支持实时内核模式调试。

可以使用！ devnode 0 1 命令显示有关设备树的信息。 有关详细信息，请参阅 [**！ devnode**](-devnode.md)。

```javascript
// PlugAndPlayDeviceTree.js
// An ES6 generator function which recursively filters the device tree looking for PCI devices in the started state.
//
function *filterDevices(deviceNode)
{
    //
    // If the device instance path has "PCI" in it and is started (state == 776), yield it from the generator.
    //
    if (deviceNode.InstancePath.indexOf("PCI") != -1 && deviceNode.State == 776)
    {
        yield deviceNode;
    }
 
    //
    // Recursively invoke the generator for all children of the device node.
    //
    for (var childNode of deviceNode.Children)
    {
        yield* filterDevices(childNode);
    }
}
 
//
// A function which finds the device tree of the first session in the debugger and passes it to our filter function.
//
function filterAllDevices()
{
    return filterDevices(host.namespace.Debugger.Sessions.First().Devices.DeviceTree.First());
}
```

建立与目标系统的内核模式连接。

```dbgcmd
0: kd> !load jsprovider.dll
```

```dbgcmd
0: kd> .scriptload c:\WinDbg\Scripts\PlugAndPlayDeviceTree.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\PlugAndPlayDeviceTree.js'
```

调用 filterAllDevices ( # A1 函数。

```dbgcmd
0: kd> dx Debugger.State.Scripts.PlugAndPlayDeviceTree.Contents.filterAllDevices()
Debugger.State.Scripts.PlugAndPlayDeviceTree.Contents.filterAllDevices()                 : [object Generator]
    [0x0]            : PCI\VEN_8086&DEV_D131&SUBSYS_304A103C&REV_11\3&21436425&0&00
    [0x1]            : PCI\VEN_8086&DEV_D138&SUBSYS_304A103C&REV_11\3&21436425&0&18 (pci)
    [0x2]            : PCI\VEN_10DE&DEV_06FD&SUBSYS_062E10DE&REV_A1\4&324c21a&0&0018 (nvlddmkm)
    [0x3]            : PCI\VEN_8086&DEV_3B64&SUBSYS_304A103C&REV_06\3&21436425&0&B0 (HECIx64)
    [0x4]            : PCI\VEN_8086&DEV_3B3C&SUBSYS_304A103C&REV_05\3&21436425&0&D0 (usbehci)
    [0x5]            : PCI\VEN_8086&DEV_3B56&SUBSYS_304A103C&REV_05\3&21436425&0&D8 (HDAudBus)
...
```

以上提供的每个对象都将自动支持 DML，并可选择与任何其他 dx 查询一样进行选择。

或者，若要使用此脚本，可以使用 LINQ 查询来实现类似的结果。

```dbgcmd
0: kd> dx @$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.InstancePath.Contains("PCI") && n.State == 776)
@$cursession.Devices.DeviceTree.Flatten(n => n.Children).Where(n => n.InstancePath.Contains("PCI") && n.State == 776)  
    [0x0]            : PCI\VEN_8086&DEV_D131&SUBSYS_304A103C&REV_11\3&21436425&0&00
    [0x1]            : PCI\VEN_8086&DEV_D138&SUBSYS_304A103C&REV_11\3&21436425&0&18 (pci)
    [0x2]            : PCI\VEN_10DE&DEV_06FD&SUBSYS_062E10DE&REV_A1\4&324c21a&0&0018 (nvlddmkm)
    [0x3]            : PCI\VEN_8086&DEV_3B64&SUBSYS_304A103C&REV_06\3&21436425&0&B0 (HECIx64)
    [0x4]            : PCI\VEN_8086&DEV_3B3C&SUBSYS_304A103C&REV_05\3&21436425&0&D0 (usbehci)
    [0x5]            : PCI\VEN_8086&DEV_3B56&SUBSYS_304A103C&REV_05\3&21436425&0&D8 (HDAudBus)
...
```

## <a name="span-idmultimediaspanspan-idmultimediaspanspan-idmultimediaspanextend-devices-specific-to-multimedia-kernel-mode"></a><span id="Multimedia"></span><span id="multimedia"></span><span id="MULTIMEDIA"></span>将特定于多媒体 (内核模式的设备扩展) 

此较大的 JavaScript 示例扩展了内核 \_ 设备 \_ 对象，以获取特定于多媒体的信息并将 StreamingDevices 添加到调试器会话。

此脚本旨在支持内核模式调试。

请注意，将会话扩展到 StreamingDevices 的选项仅用于示例目的。 此名称应仅保留到 \_ "设备对象" 或在现有的 " \_ 命名空间" 中更深。设备。 \* 层次结构.

```javascript
// StreamingFinder.js
// Extends a kernel _DEVICE_OBJECT for information specific to multimedia 
// and adds StreamingDevices to a debugger session.
//

"use strict";
 
function initializeScript()
{
    // isStreamingDeviceObject: 
    //
    // Returns whether devObj (as a _DEVICE_OBJECT -- not a pointer) looks like it is a device
    // object for a streaming device.
    //
    function isStreamingDeviceObject(devObj)
    {
        try
        {
            var devExt = devObj.DeviceExtension;
            var possibleStreamingExtPtrPtr = host.createPointerObject(devExt.address, "ks.sys", "_KSIDEVICE_HEADER **", devObj);
            var possibleStreamingExt = possibleStreamingExtPtrPtr.dereference().dereference();
            var baseDevice = possibleStreamingExt.BaseDevice;
 
            if (devObj.targetLocation == baseDevice.dereference().targetLocation)
            {
                return true;
            }
        }
        //
        // The above code expects to fail (walking into invalid or paged out memory) often.  A failure to read the memory
        // of the target process will result in an exception.  Catch such exception and indicate that the object does not
        // match the profile of a "streaming device object".
        //
        catch(exc)
        {   
        }
 
        return false;
    }
 
    // findStreamingFDO(pdo):
    //
    // From a physical device object, walks up the device stack and attempts to find a device which
    // looks like a streaming device (and is thus assumed to be the FDO).  pdo is a pointer to 
    // the _DEVICE_OBJECT for the pdo.
    //
    function findStreamingFDO(pdo)
    {
        for (var device of pdo.UpperDevices)
        {
            if (isStreamingDeviceObject(device.dereference()))
            {
                return device;
            }
        }
 
        return null;
    }
 
    // streamingDeviceList:
    //
    // A class which enumerates all streaming devices on the system.
    //
    class streamingDeviceList
    {
        constructor(session)
        {
            this.__session = session;
        }
 
        *[Symbol.iterator]()
        {
            //
            // Get the list of all PDOs from PNP using LINQ:
            //
            var allPDOs = this.__session.Devices.DeviceTree.Flatten(function(dev) { return dev.Children; })
                                                           .Select (function(dev) { return dev.PhysicalDeviceObject; });
 
            //
            // Walk the stack up each PDO to find the functional device which looks like a KS device.  This is
            // a very simple heuristic test: the back pointer to the device in the KS device extension is
            // accurate.  Make sure this is wrapped in a try/catch to avoid invalid memory reads causing
            // us to bail out.
            //
            // Don't even bother checking the PDO.
            //
            for (var pdo of allPDOs)
            {
                var fdo = findStreamingFDO(pdo);
                if (fdo != null)
                {
                    yield fdo;
                }
            }
        }
   }
 
    // streamingDeviceExtension:
    //
    // An object which will extend "session" and include the list of streaming devices.
    //
    class streamingDeviceExtension
    {
        get StreamingDevices()
        {
            return new streamingDeviceList(this);
        }
    };
 
    // createEntryList:
    //
    // An abstraction over the create entry list within a streaming device.
    //    
    class createEntryList
    {
        constructor(ksHeader)
        {
            this.__ksHeader = ksHeader;
        }
 
        *[Symbol.iterator]()
        {
            for (var entry of host.namespace.Debugger.Utility.Collections.FromListEntry(this.__ksHeader.ChildCreateHandlerList, "ks!KSICREATE_ENTRY", "ListEntry"))
            {
                                                            if (!entry.CreateItem.Create.isNull)
                {
                    yield entry;
                }
            }
        }
    }
 
    // streamingInformation:
    //
    // Represents the streaming state of a device.
    //    
    class streamingInformation
    {
        constructor(fdo)
        {
            this.__fdo = fdo;
 
            var devExt = fdo.DeviceExtension;
            var streamingExtPtrPtr = host.createPointerObject(devExt.address, "ks.sys", "_KSIDEVICE_HEADER **", fdo);
            this.__ksHeader = streamingExtPtrPtr.dereference().dereference();
        }
 
        get CreateEntries()
        {
            return new createEntryList(this.__ksHeader);
        }
    }
 
    // createEntryVisualizer:
    //
    // A visualizer for KSICREATE_ENTRY
    //
    class createEntryVisualizer
    {
        toString()
        {
            return this.CreateItem.ObjectClass.toString();
        }
 
        get CreateContext()
        {
            //
            // This is probably not entirely accurate.  The context is not *REQUIRED* to be an IUnknown.
            // More analysis should probably be performed.
            //
            return host.createTypedObject(this.CreateItem.Context.address, "ks.sys", "IUnknown", this);
        }
    }
 
    // deviceExtension:
    //
    // Extends our notion of a device in the device tree to place streaming information on
    // top of it.
    //
    class deviceExtension
    {
        get StreamingState()
        {
            if (isStreamingDeviceObject(this))
            {
                return new streamingInformation(this);
            }
 
            //
            // If we cannot find a streaming FDO, returning undefined will indicate that there is no value
            // to the property.
            //
            return undefined;
        }
    }
 
    return [new host.namedModelParent(streamingDeviceExtension, "Debugger.Models.Session"),
            new host.typeSignatureExtension(deviceExtension, "_DEVICE_OBJECT"),
            new host.typeSignatureRegistration(createEntryVisualizer, "KSICREATE_ENTRY")]
}
```

首先加载脚本提供程序，如前文所述。 然后加载脚本。

```dbgcmd
0: kd> .scriptload c:\WinDbg\Scripts\StreamingFinder.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\StreamingFinder.js'
```

然后，使用 dx 命令访问脚本提供的新的 StreamingDevices 功能。

```dbgcmd
0: kd> dx -r3 @$cursession.StreamingDevices.Select(d => d->StreamingState.CreateEntries)
@$cursession.StreamingDevices.Select(d => d->StreamingState.CreateEntries)                
    [0x0]            : [object Object]
        [0x0]            : "e0HDMIOutTopo" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortTopology]
    [0x1]            : [object Object]
        [0x0]            : "AnalogDigitalCaptureTopo" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortTopology]
        [0x1]            : "AnalogDigitalCapture1Topo" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortTopology]
        [0x2]            : "AnalogDigitalCapture2Topo" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortTopology]
        [0x3]            : "AnalogDigitalCapture2Wave" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortWaveRT]
        [0x4]            : "HeadphoneTopo" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortTopology]
        [0x5]            : "RearLineOutTopo" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortTopology]
        [0x6]            : "RearLineOutWave" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: CPortWaveRT]
    [0x2]            : [object Object]
        [0x0]            : "GLOBAL" [Type: KSICREATE_ENTRY]
            [<Raw View>]     [Type: KSICREATE_ENTRY]
            CreateContext    [Type: IUnknown]
```

## <a name="span-idbusspanspan-idbusspanspan-idbusspanadding-bus-information-to-_device_object-kernel-mode"></a><span id="Bus"></span><span id="bus"></span><span id="BUS"></span> (内核模式将总线信息添加到 \_ 设备 \_ 对象) 


此脚本 \_ 对设备对象的可视化 \_ 进行扩展，以添加一个 BusInformation 字段，该字段下有 PCI 特定信息。 本示例的方式和 namespacing 仍在讨论。 它应被视为 JavaScript 提供程序功能的一个示例。

此脚本旨在支持内核模式调试。

```javascript
"use strict";

/*************************************************
DeviceExtensionInformation.js:

An example which extends _DEVICE_OBJECT to add bus specific information
to each device object.

NOTE: The means of conditionally adding and the style of namespacing this
are still being discussed.  This currently serves as an example of the capability
of JavaScript extensions.

*************************************************/

function initializeScript()
{
    // __getStackPDO():
    //
    // Returns the physical device object of the device stack whose device object
    // is passed in as 'devObj'.
    //
    function __getStackPDO(devObj)
    {
        var curDevice = devObj;
        var nextDevice = curDevice.DeviceObjectExtension.AttachedTo;
        while (!nextDevice.isNull)
        {
            curDevice = nextDevice;
            nextDevice = curDevice.DeviceObjectExtension.AttachedTo;
        }
        return curDevice;
    }
    
    // pciInformation:
    //
    // Class which abstracts our particular representation of PCI information for a PCI device or bus
    // based on a _PCI_DEVICE structure or a _PCI_BUS structure.
    //
    class pciInformation
    {
        constructor(pciDev)
        {
            this.__pciDev = pciDev;
            this.__pciPDO = __getStackPDO(this.__pciDev);
            this.__isBridge = (this.__pciDev.address != this.__pciPDO.address);
            
            if (this.__isBridge)
            {
                this.__deviceExtension = host.createTypedObject(this.__pciPDO.DeviceExtension.address, "pci.sys", "_PCI_DEVICE", this.__pciPDO);
                this.__busExtension = host.createTypedObject(this.__pciDev.DeviceExtension.address, "pci.sys", "_PCI_BUS", this.__pciPDO);
                
                this.__hasDevice = (this.__deviceExtension.Signature == 0x44696350); /* 'PciD' */
                this.__hasBus = (this.__busExtension.Signature == 0x42696350); /* 'PciB' */
                
                if (!this.__hasDevice && !this.__hasBus)
                {
                    throw new Error("Unrecognized PCI device extension");
                }
            }
            else
            {
                this.__deviceExtension = host.createTypedObject(this.__pciPDO.DeviceExtension.address, "pci.sys", "_PCI_DEVICE", this.__pciPDO);
                
                this.__hasDevice = (this.__deviceExtension.Signature == 0x44696350); /* 'PciD' */
                this.__hasBus = false;
                
                if (!this.__hasDevice)
                {
                    throw new Error("Unrecognized PCI device extension");
                }
            }
        }
        
        toString()
        {
            
            if (this.__hasBus && this.__hasDevice)
            {
                return "Bus: " + this.__busExtension.toString() + " Device: " + this.__deviceExtension.toString();
            }
            else if (this.__hasBus)
            {
                return this.__busExtension.toString();
            }
            else
            {
                return this.__deviceExtension.toString();
            }
        }
        
        get Device()
        {
            if (this.__hasDevice)
            {
                // NatVis supplies the visualization for _PCI_DEVICE
                return this.__deviceExtension;
            }
            
            return undefined;
        }
        
        get Bus()
        {
            if (this.__hasBus)
            {
                // NatVis supplies the visualization for _PCI_BUS
                return this.__busExtension;
            }
            
            return undefined;
        }
    }
    
    // busInformation:
    //
    // Our class which does analysis of what bus a particular device is on and places information about
    // about that bus within the _DEVICE_OBJECT visualization.
    //
    class busInformation
    {
        constructor(devObj)
        {
            this.__devObj = devObj;
        }
        
        get PCI()
        {
            //
            // Check the current device object.  This may be a PCI bridge
            // in which both the FDO and PDO are relevant (one for the bus information
            // and one for the bridge device information).
            //
            var curName = this.__devObj.DriverObject.DriverName.toString();
            if (curName.includes("\\Driver\\pci"))
            {
                return new pciInformation(this.__devObj);
            }
            
            var stackPDO = __getStackPDO(this.__devObj);
            var pdoName = stackPDO.DriverObject.DriverName.toString();
            if (pdoName.includes("\\Driver\\pci"))
            {
                return new pciInformation(stackPDO);
            }
            
            return undefined;
        }
    }
    
    // busInformationExtension:
    //
    // An extension placed on top of _DEVICE_OBJECT in order to provide bus analysis and bus specific
    // information to the device.
    //
    class busInformationExtension
    {
        get BusInformation()
        {
            return new busInformation(this);
        }
    }
    
    return [new host.typeSignatureExtension(busInformationExtension, "_DEVICE_OBJECT")];
}
```

首先加载脚本提供程序，如前文所述。 然后加载脚本。

```dbgcmd
0: kd> .scriptload c:\WinDbg\Scripts\DeviceExtensionInformation.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\DeviceExtensionInformation.js'
```

我们需要找到感兴趣的设备对象的地址。 在此示例中，我们将检查音频 HDAudBus 驱动程序。

```dbgcmd
0: kd>  !drvobj HDAudBus
Driver object (ffffb60757a4ae60) is for:
 \Driver\HDAudBus
Driver Extension List: (id , addr)
(fffff8050a9eb290 ffffb60758413180)  
Device Object list:
ffffb60758e21810  ffffb60757a67c60
```

加载脚本后，使用 dx 命令显示设备对象的总线信息。

```dbgcmd
0: kd> dx -r1 (*((ntkrnlmp!_DEVICE_OBJECT *)0xffffe00001b567c0))
(*((ntkrnlmp!_DEVICE_OBJECT *)0xffffe00001b567c0))                 : Device for "\Driver\HDAudBus" [Type: _DEVICE_OBJECT]
    [<Raw View>]     [Type: _DEVICE_OBJECT]
    Flags            : 0x2004
    UpperDevices     : None
    LowerDevices     : Immediately below is Device for "\Driver\ACPI" [at 0xffffe000003d9820]
    Driver           : 0xffffe00001ccd060 : Driver "\Driver\HDAudBus" [Type: _DRIVER_OBJECT *]
    BusInformation   : [object Object]

0: kd> dx -r1 (*((ntkrnlmp!_DEVICE_OBJECT *)0xffffe00001b567c0)).@"BusInformation"
(*((ntkrnlmp!_DEVICE_OBJECT *)0xffffe00001b567c0)).@"BusInformation"                 : [object Object]
    PCI              :  (d=0x14 f=0x2) Vendor=0x1022 Device=0x780d Multimedia Device / Unknown Sub Class

0: kd> dx -r1 (*((ntkrnlmp!_DEVICE_OBJECT *)0xffffe00001b567c0)).@"BusInformation".@"PCI"
(*((ntkrnlmp!_DEVICE_OBJECT *)0xffffe00001b567c0)).@"BusInformation".@"PCI"                 :  (d=0x14 f=0x2) Vendor=0x1022 Device=0x780d Multimedia Device / Unknown Sub Class
    Device           :  (d=0x14 f=0x2) Vendor=0x1022 Device=0x780d Multimedia Device / Unknown Sub Class [Type: _PCI_DEVICE]

0: kd> dx -r1 (*((pci!_PCI_DEVICE *)0xffffe000003fe1b0))
(*((pci!_PCI_DEVICE *)0xffffe000003fe1b0))                 :  (d=0x14 f=0x2) Vendor=0x1022 Device=0x780d Multimedia Device / Unknown Sub Class [Type: _PCI_DEVICE]
    [<Raw View>]     [Type: _PCI_DEVICE]
    Device           : 0xffffe000003fe060 : Device for "\Driver\pci" [Type: _DEVICE_OBJECT *]
    Requirements    
    Resources       

0: kd> dx -r1 (*((pci!_PCI_DEVICE *)0xffffe000003fe1b0)).@"Resources"
(*((pci!_PCI_DEVICE *)0xffffe000003fe1b0)).@"Resources"                
    BaseAddressRegisters
    Interrupt        : Line Based -- Interrupt Line = 0x10 [Type: _PCI_DEVICE_INTERRUPT_RESOURCE]

0: kd> dx -r1 (*((pci!_PCI_DEVICE *)0xffffe000003fe1b0)).@"Resources".@"BaseAddressRegisters"
(*((pci!_PCI_DEVICE *)0xffffe000003fe1b0)).@"Resources".@"BaseAddressRegisters"                
    [0x0]            : Memory Resource: 0xf0340000 of length 0x4000 [Type: _CM_PARTIAL_RESOURCE_DESCRIPTOR]
```

## <a name="span-idtitlespanspan-idtitlespanspan-idtitlespanfind-an-application-title-user-mode"></a><span id="Title"></span><span id="title"></span><span id="TITLE"></span> (用户模式下查找应用程序标题) 


此示例将循环访问调试器的当前进程中的所有线程，查找包含* \_ \_ mainCRTStartup*的帧，然后在 CRT 的启动期间返回 StartupInfo 中的字符串。 此脚本显示 JavaScript 中的迭代、字符串操作和 LINQ 查询的示例。

此脚本旨在支持用户模式调试。

```javascript
// TitleFinder.js
// A function which uses just JavaScript concepts to find the title of an application
//
function findTitle()
{
    var curProcess = host.currentProcess;
    for (var thread of curProcess.Threads)
    {
        for (var frame of thread.Stack.Frames)
        {
            if (frame.toString().includes("__mainCRTStartup"))
            {
                var locals = frame.LocalVariables;
 
                //
                // locals.StartupInfo.lpTitle is just an unsigned short *.  We need to actually call an API to
                // read the UTF-16 string in the target address space.  This would be true even if this were
                // a char* or wchar_t*.
                //
                return host.memory.readWideString(locals.StartupInfo.lpTitle);
            }
        }
    }
}
 
//
// A function which uses both JavaScript and integrated LINQ concepts to do the same.
//
function findTitleWithLINQ()
{
    var isMainFrame = function(frame) { return frame.toString().includes("__mainCRTStartup"); };
    var isMainThread = function(thread) { return thread.Stack.Frames.Any(isMainFrame); };
 
    var curProcess = host.currentProcess;
    var mainThread = curProcess.Threads.Where(isMainThread).First();
    var mainFrame = mainThread.Stack.Frames.Where(isMainFrame).First();
 
    var locals = mainFrame.LocalVariables;
 
    //
    // locals.StartupInfo.lpTitle is just an unsigned short *.  We need to actually call an API to
    // read the UTF-16 string in the target address space.  This would be true even if this were
    // a char* or wchar_t*.
    //
    return host.memory.readWideString(locals.StartupInfo.lpTitle);
}
```

```dbgcmd
0: kd> .scriptload c:\WinDbg\Scripts\TitleFinder.js
JavaScript script successfully loaded from 'c:\WinDbg\Scripts\TitleFinder.js'
```

调用 findTitle ( # A1 函数将返回 notepad.exe

```dbgcmd
0:000> dx Debugger.State.Scripts.TitleFinder.Contents.findTitle()
Debugger.State.Scripts.TitleFinder.Contents.findTitle() : C:\Windows\System32\notepad.exe
```

调用 LINQ 版本时，findTitleWithLINQ ( # A1 还会返回 notepad.exe

```dbgcmd
0:000> dx Debugger.State.Scripts.TitleFinder.Contents.findTitleWithLINQ()
Debugger.State.Scripts.titleFinder.Contents.findTitleWithLINQ() : C:\Windows\System32\notepad.exe
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[JavaScript 调试器脚本](javascript-debugger-scripting.md)

 

 






