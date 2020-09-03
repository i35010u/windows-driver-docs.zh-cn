---
title: 将事件跟踪添加到内核模式驱动程序
description: 将事件跟踪添加到内核模式驱动程序
ms.assetid: 74fdb4b2-aad1-4d8a-b146-40a92e1fdbb5
keywords:
- Windows WDK 事件跟踪，内核模式
- ETW WDK，内核模式
- 内核模式 ETW WDK 软件跟踪
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 9e817ba497623456e121991fddb43e1bdfceafac
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384181"
---
# <a name="adding-event-tracing-to-kernel-mode-drivers"></a>将事件跟踪添加到内核模式驱动程序

本部分介绍如何使用 Windows 事件跟踪 (ETW) 内核模式 API 向内核模式驱动程序添加事件跟踪。 ETW 内核模式 API 随 Windows Vista 一起引入，在早期版本的操作系统中不受支持。 如果驱动程序需要在 Windows 2000 和更高版本中支持跟踪功能，请使用 [WPP 软件跟踪](wpp-software-tracing.md) 或 [WMI 事件跟踪](../kernel/wmi-event-tracing.md) 。

> [!TIP]
> 若要查看演示如何使用 Windows 驱动程序工具包 (WDK) 8.1 和 Visual Studio 实现 ETW 的示例代码，请参阅 [Eventdrv 示例](/samples/microsoft/windows-driver-samples/eventdrv/)。

本部分内容：

- [工作流-向内核模式驱动程序添加事件跟踪](#workflow---adding-event-tracing-to-kernel-mode-drivers)

- [1. 确定要引发的事件类型以及发布事件的位置](#1-decide-the-type-of-events-to-raise-and-where-to-publish-them)

- [2. 创建定义提供程序、事件和通道的检测清单](#2-create-an-instrumentation-manifest-that-defines-the-provider-the-events-and-channels)

- [3. 使用消息编译器编译检测清单 ( # A0) ](#3-compile-the-instrumentation-manifest-by-using-the-message-compiler-mcexe)

- [4. 添加生成的代码以引发 (发布) 事件 (注册、注销和写入事件) ](#4-add-the-generated-code-to-raise-publish-the-events-register-unregister-and-write-events)

- [5. 构建驱动程序](#5-build-the-driver)

- [6. 安装清单](#6-install-the-manifest)

- [7. 测试驱动程序以验证 ETW 支持](#7-test-the-driver-to-verify-etw-support)

## <a name="workflow---adding-event-tracing-to-kernel-mode-drivers"></a>工作流-向内核模式驱动程序添加事件跟踪

![向内核模式驱动程序添加事件跟踪的过程概述。](images/etw-km-process.png)

## <a name="1-decide-the-type-of-events-to-raise-and-where-to-publish-them"></a>1. 确定要引发的事件类型以及发布事件的位置

开始编码之前，必须确定希望驱动程序通过 Windows (ETW) 的事件跟踪记录的事件类型。 例如，你可能需要记录事件，这些事件可帮助你在驱动程序分发后诊断问题，或可能有助于你开发驱动程序的事件。 事件的类型用通道标识。 *通道*是一种名为 "管理员"、"操作"、"分析" 或 "调试" 的事件流，该事件面向特定受众，类似于电视频道。 通道将事件提供程序中的事件传递到事件日志和事件使用者。 有关信息，请参阅 [Windows 事件日志参考](/windows/win32/wes/windows-event-log-reference)。

在开发过程中，您很可能对跟踪有助于调试代码的事件感兴趣。 可以在生产代码中使用此相同的通道，以帮助对部署驱动程序后可能出现的问题进行故障排除。 你可能还需要跟踪可用于衡量性能的事件;这些事件可帮助 IT 专业人员精细优化服务器性能，并帮助确定网络瓶颈。

## <a name="2-create-an-instrumentation-manifest-that-defines-the-provider-the-events-and-channels"></a>2. 创建定义提供程序、事件和通道的检测清单

检测清单是一个 XML 文件，它提供提供程序将引发的事件的正式说明。 检测清单会标识事件提供程序，指定通道或通道 (多达八个) ，并描述事件使用的事件和模板。 此外，检测清单还允许对字符串进行本地化，因此你可以本地化跟踪消息。 事件系统和事件使用者可以利用清单中提供的结构化 XML 数据执行查询和分析。

有关检测清单的详细信息，请参阅 [ (windows) 中编写检测清单 ](/windows/desktop/WES/writing-an-instrumentation-manifest) 和 [使用 windows 事件日志 (windows) ](/windows/desktop/WES/using-windows-event-log)。

> [!NOTE]
> 尽管可以手动创作检测清单，但在 \\ \\ \\ \\ \\ 安装 WDK 和 Visual Studio 时，应考虑使用% WindowsSdkDir% bin x64% WindowsSdkDir% bin x86 文件夹中包含的 ECManGen.exe 工具。 % WindowsSdkDir% 表示安装此 WDK 版本的 Windows 工具包目录的路径，例如，C： \\ Program Files (x86) \\ Windows 工具包 \\ 8.1。 ECManGen.exe 是一种应用程序，可引导你从头开始创建清单，而无需使用 XML 标记。 使用该工具时，请了解 [ (windows) ](/windows/desktop/WES/writing-an-instrumentation-manifest) 部分和在 [EventManifest 架构 (Windows) ](/windows/desktop/WES/eventmanifestschema-schema) 部分编写规范清单中的信息。

以下检测清单显示了一个使用名称 "示例驱动程序" 的事件提供程序。 请注意，此名称不必与驱动程序二进制文件的名称相同。 该清单还指定了提供程序的 GUID 和消息和资源文件的路径。 消息和资源文件 let ETW 知道在何处查找对事件进行解码和报告所需的资源。 这些路径指向驱动程序 ( .sys) 文件的位置。 必须在目标计算机上的指定目录中安装驱动程序。

该示例使用命名通道 **系统**，即 **Admin**类型事件的通道。此通道在 Winmeta.xml 文件中定义，该文件随 Windows 驱动程序)  (工具包在% WindowsSdkDir% \\ include \\ um 目录中提供。 **系统**通道对于在系统服务帐户下运行的应用程序是安全的。 清单包含事件模板，用于描述在发布事件时提供的数据类型及其静态和动态内容。 此示例清单定义了三个事件： `StartEvent` 、 `SampleEventA` 和 `UnloadEvent` 。

除了通道以外，还可以将事件与级别和关键字关联起来。 使用关键字和级别可以启用事件，并提供一种机制，用于在发布事件时筛选事件。 关键字可用于将逻辑上相关的事件组合在一起。 级别可用于指示事件的严重级别或详细级别，例如 "严重"、"错误"、"警告" 或 "信息"。 Winmeta.xml 文件包含事件属性的预定义值。

为事件负载 (事件消息和数据) 创建模板时，必须指定输入和输出类型。 [** (Windows) 的 InputType 复杂类型**](/windows/desktop/WES/eventmanifestschema-inputtype-complextype)的 "备注" 部分介绍了支持的类型。

```XML
<?xml version='1.0' encoding='utf-8' standalone='yes'?>
<instrumentationManifest
    xmlns="http://schemas.microsoft.com/win/2004/08/events"
    xmlns:win="http://manifests.microsoft.com/win/2004/08/windows/events"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://schemas.microsoft.com/win/2004/08/events eventman.xsd"
    >
  <instrumentation>
    <events>
      <provider
          guid="{b5a0bda9-50fe-4d0e-a83d-bae3f58c94d6}"
          messageFileName="%SystemDrive%\ETWDriverSample\Eventdrv.sys"
          name="Sample Driver"
          resourceFileName="%SystemDrive%\ETWDriverSample\Eventdrv.sys"
          symbol="DriverControlGuid"
          >
        <channels>
          <importChannel
              chid="SYSTEM"
              name="System"
              />
        </channels>
        <templates>
          <template tid="tid_load_template">
            <data
                inType="win:UInt16"
                name="DeviceNameLength"
                outType="xs:unsignedShort"
                />
            <data
                inType="win:UnicodeString"
                name="name"
                outType="xs:string"
                />
            <data
                inType="win:UInt32"
                name="Status"
                outType="xs:unsignedInt"
                />
          </template>
          <template tid="tid_unload_template">
            <data
                inType="win:Pointer"
                name="DeviceObjPtr"
                outType="win:HexInt64"
                />
          </template>
        </templates>
        <events>
          <event
              channel="SYSTEM"
              level="win:Informational"
              message="$(string.StartEvent.EventMessage)"
              opcode="win:Start"
              symbol="StartEvent"
              template="tid_load_template"
              value="1"
              />
          <event
              channel="SYSTEM"
              level="win:Informational"
              message="$(string.SampleEventA.EventMessage)"
              opcode="win:Info"
              symbol="SampleEventA"
              value="2"
              />
          <event
              channel="SYSTEM"
              level="win:Informational"
              message="$(string.UnloadEvent.EventMessage)"
              opcode="win:Stop"
              symbol="UnloadEvent"
              template="tid_unload_template"
              value="3"
              />
        </events>
      </provider>
    </events>
  </instrumentation>
  <localization xmlns="http://schemas.microsoft.com/win/2004/08/events">
    <resources culture="en-US">
      <stringTable>
        <string
            id="StartEvent.EventMessage"
            value="Driver Loaded"
            />
        <string
            id="SampleEventA.EventMessage"
            value="IRP A Occurred"
            />
        <string
            id="UnloadEvent.EventMessage"
            value="Driver Unloaded"
            />
      </stringTable>
    </resources>
  </localization>
</instrumentationManifest>
```

## <a name="3-compile-the-instrumentation-manifest-by-using-the-message-compiler-mcexe"></a>3. 使用消息编译器编译检测清单 ( # A0) 

在编译源代码之前，必须运行 [消息编译器 ( # A0) ](/windows/desktop/WES/message-compiler--mc-exe-) 。 消息编译器包含在 (WDK) 的 Windows 驱动程序工具包中。 消息编译器会创建一个标头文件，其中包含事件提供程序、事件特性、信道和事件的定义。 你必须在源代码中包括此头文件。 消息编译器还会将生成的资源编译器脚本 (\*) 和生成的 bin 文件 (包含资源编译器脚本的) 二进制资源。

可以通过以下几种方式将此步骤包含在生成过程中：

- 将消息编译器任务添加到驱动程序项目文件 (如 [Eventdrv 示例](/samples/microsoft/windows-driver-samples/eventdrv/)) 中所示。

- 使用 Visual Studio 添加检测清单并配置消息编译器属性。

**将消息编译器任务添加到项目文件** 有关如何在生成过程中包括消息编译器的示例，请查看 [Eventdrv 示例](/samples/microsoft/windows-driver-samples/eventdrv/)的项目文件。 在 Eventdrv. .vcxproj 文件中，有一个调用消息编译器的** &lt; MessageCompile &gt; **部分。 消息编译器使用清单文件 ( # A0) 作为输入来生成头文件 evntdrvEvents。 此部分还指定生成的 RC 文件的路径，并启用内核模式日志记录宏。 你可以复制此部分，并将其添加到你的驱动程序项目文件 () 。

```XML

    <MessageCompile Include="evntdrv.xml">
      <GenerateKernelModeLoggingMacros>true</GenerateKernelModeLoggingMacros>
      <HeaderFilePath>.\$(IntDir)</HeaderFilePath>
      <GeneratedHeaderPath>true</GeneratedHeaderPath>
      <WinmetaPath>"$(SDK_INC_PATH)\winmeta.xml"</WinmetaPath>
      <RCFilePath>.\$(IntDir)</RCFilePath>
      <GeneratedRCAndMessagesPath>true</GeneratedRCAndMessagesPath>
      <GeneratedFilesBaseName>evntdrvEvents</GeneratedFilesBaseName>
      <UseBaseNameOfInput>true</UseBaseNameOfInput>
    </MessageCompile>
```

生成 Eventdrv.sys 示例时，Visual Studio 将为事件跟踪创建必要的文件。 它还会将 evntdrv.xml 清单添加到驱动程序项目的资源列表文件中。 您可以选择并按住 (或右键单击) 清单以查看消息编译器属性页。

### <a name="using-visual-studio-to-add-the-instrumentation-manifest"></a>使用 Visual Studio 添加检测清单

可以将检测清单添加到驱动程序项目，然后配置消息编译器属性以生成必要的资源和标头文件。

### <a name="to-add-the-instrumentation-manifest-to-the-project-using-visual-studio"></a>使用 Visual Studio 将检测清单添加到项目中

1. 在解决方案资源管理器中，将清单文件添加到驱动程序项目。 选择并按住 (或右键单击) **资源文件 " &gt; 添加 &gt; 现有项** (例如，evntdrv.xml 或 mydriver) 。

2. 选择并按住 (或右键单击) 刚才添加的文件，然后使用属性页将项类型更改为 **MessageCompile** ，然后选择 " **应用**"。

3. 消息编译器属性随即出现。 在 " **常规** 设置" 下，设置以下选项，然后选择 " **应用**"。

    | 常规                                 | 设置       |
    |-----------------------------------------|---------------|
    | **生成内核模式日志记录宏** | **是 (-公里) ** |
    | **使用输入的基名称**              | **是 (-b) **  |

4. 在 " **文件选项**" 下，设置以下选项，然后选择 " **应用**"。

    | 文件选项                                    | 设置         |
    |-------------------------------------------------|-----------------|
    | **生成包含计数器的标头文件** | **是**         |
    | **头文件路径**                            | **$(IntDir)**   |
    | **生成 RC 和二进制消息文件路径**  | **是**         |
    | **RC 文件路径**                                | **$(IntDir)**   |
    | **生成文件基名**                   | **$ (文件名) ** |

默认情况下，消息编译器使用输入文件的基名称作为它生成的文件的基名称。 若要指定基名称，请将 **生成的文件基名称** 设置 (-z) 字段。 在 Eventdr.sys 示例中，基名称设置为 *evntdrvEvents* ，以便它与 evntdrv 中包含的头文件 evntdrvEvents 的名称相匹配。

> [!NOTE]
> 如果你在 Visual Studio 项目中未包含生成的 .rc 文件，则可能会收到有关在安装清单文件时找不到的资源的错误消息。

## <a name="4-add-the-generated-code-to-raise-publish-the-events-register-unregister-and-write-events"></a>4. 添加生成的代码以引发 (发布) 事件 (注册、注销和写入事件) 

在检测清单中，定义了事件提供程序和事件说明符的名称。 使用消息编译器编译检测清单时，消息编译器会生成一个标头文件，该文件描述资源并定义事件的宏。 现在，必须将生成的代码添加到驱动程序以引发这些事件。

1. 在源文件中，包含由消息编译器生成 ( # A0) 的事件标头文件。 例如，在 [Eventdrv 示例](/samples/microsoft/windows-driver-samples/eventdrv/)中，Evntdrv 源文件包含上一步骤中生成的 (evntdrvEvents) 的标头文件：

   ```c++
   #include "evntdrvEvents.h"  
   ```

2. 添加宏，用于注册驱动程序并将其注销作为事件提供程序。 例如，在 [Eventdrv 示例](/samples/microsoft/windows-driver-samples/eventdrv/) 的标头文件中 (evntdrvEvents) 时，消息编译器将根据提供程序的名称创建宏。 在清单中， [Eventdrv 示例](/samples/microsoft/windows-driver-samples/eventdrv/) 使用名为 "sample Driver" 作为提供程序的名称。 消息编译器将提供程序的名称与事件宏组合在一起，以注册提供程序，在本例中为 **EventRegisterSample \_ 驱动程序**。

   ```ManagedCPlusPlus
   //  This is the generated header file envtdrvEvents.h
   //
   //  ...
   //
   //
   // Register with ETW Vista +
   //
   #ifndef EventRegisterSample_Driver
   #define EventRegisterSample_Driver() McGenEventRegister(&DriverControlGuid, McGenControlCallbackV2, &DriverControlGuid_Context, &Sample_DriverHandle)
   #endif
   ```

   将**EventRegister \<*provider*\> **宏添加到[*DriverEntry*](../wdf/driverentry-for-kmdf-drivers.md)函数。 将此函数添加到创建和初始化设备对象的代码之后。 请注意，必须通过调用**EventUnregister \<*provider*\> **来匹配**对 \<*provider*\> EventRegister**函数的调用。 你可以在驱动程序的[ </em> *卸载* * ](<https://msdn.microsoft.com/library/windows/hardware/ff564886>)例程中注销该驱动程序。

   ```ManagedCPlusPlus
      // DriverEntry function
      // ...


       // Register with ETW
       //
       EventRegisterSample_Driver();
    ```

3. 将生成的代码添加到驱动程序的源文件，以写入 (引发) 在清单中指定的事件。 从清单中编译的标头文件包含驱动程序的生成代码。 使用标头文件中定义的**EventWrite \<*event*\> **函数将跟踪消息发布到 ETW。 例如，下面的代码显示 evntdrvEvents 中为 [Eventdrv 示例](/samples/microsoft/windows-driver-samples/eventdrv/)定义的事件的宏。

   用于编写这些事件的宏称为： `EventWriteStartEvent` 、 `EventWriteSampleEventA` 和 `EventWriteUnloadEvent` 。 如您在这些宏的定义中所看到的，宏定义会自动包含一个**EventEnabled \<*event*\> **宏，用于检查是否已启用该事件。 如果未启用该事件，则检查将不再需要生成有效负载。

   ```ManagedCPlusPlus

   ///
   // This is the generated header file envtdrvEvents.h
   //
   //  ...
   //
   // Enablement check macro for StartEvent
   //

   #define EventEnabledStartEvent() ((Sample_DriverEnableBits[0] & 0x00000001) != 0)

   //
   // Event Macro for StartEvent
   //
   #define EventWriteStartEvent(Activity, DeviceNameLength, name, Status)\
           EventEnabledStartEvent() ?\
           Template_hzq(Sample_DriverHandle, &StartEvent, Activity, DeviceNameLength, name, Status)\
           : STATUS_SUCCESS\

   //
   // Enablement check macro for SampleEventA
   //

   #define EventEnabledSampleEventA() ((Sample_DriverEnableBits[0] & 0x00000001) != 0)

   //
   // Event Macro for SampleEventA
   //
   #define EventWriteSampleEventA(Activity)\
           EventEnabledSampleEventA() ?\
           TemplateEventDescriptor(Sample_DriverHandle, &SampleEventA, Activity)\
           : STATUS_SUCCESS\

   //
   // Enablement check macro for UnloadEvent
   //

   #define EventEnabledUnloadEvent() ((Sample_DriverEnableBits[0] & 0x00000001) != 0)

   //
   // Event Macro for UnloadEvent
   //
   #define EventWriteUnloadEvent(Activity, DeviceObjPtr)\
           EventEnabledUnloadEvent() ?\
           Template_p(Sample_DriverHandle, &UnloadEvent, Activity, DeviceObjPtr)\
           : STATUS_SUCCESS\
  
    ```

   将**EventWrite \<*event*\> **宏添加到要引发事件的源代码中。 例如，以下代码片段显示了[Eventdrv 示例](/samples/microsoft/windows-driver-samples/eventdrv/)中的[*DriverEntry*](../wdf/driverentry-for-kmdf-drivers.md)例程。 *DriverEntry*包括用于向 Etw (*EventRegisterSample \_ 驱动程序*注册驱动程序的宏) ，以及用于将驱动程序事件写入 etw (*EventWriteStartEvent*) 的宏。

   ```ManagedCPlusPlus
   NTSTATUS
   DriverEntry(
       IN PDRIVER_OBJECT DriverObject,
       IN PUNICODE_STRING RegistryPath
       )
   /*++

   Routine Description:

       Installable driver initialization entry point.
       This entry point is called directly by the I/O system.

   Arguments:

       DriverObject - pointer to the driver object

       RegistryPath - pointer to a unicode string representing the path
           to driver-specific key in the registry

   Return Value:

      STATUS_SUCCESS if successful
      STATUS_UNSUCCESSFUL  otherwise

   --*/
   {
       NTSTATUS Status = STATUS_SUCCESS;
       UNICODE_STRING DeviceName;
       UNICODE_STRING LinkName;
       PDEVICE_OBJECT EventDrvDeviceObject;
       WCHAR DeviceNameString[128];
       ULONG LengthToCopy = 128 * sizeof(WCHAR);
       UNREFERENCED_PARAMETER (RegistryPath);

       KdPrint(("EventDrv: DriverEntry\n"));

       //
       // Create Dispatch Entry Points.  
       //
       DriverObject->DriverUnload = EventDrvDriverUnload;
       DriverObject->MajorFunction[ IRP_MJ_CREATE ] = EventDrvDispatchOpenClose;
       DriverObject->MajorFunction[ IRP_MJ_CLOSE ] = EventDrvDispatchOpenClose;
       DriverObject->MajorFunction[ IRP_MJ_DEVICE_CONTROL ] = EventDrvDispatchDeviceControl;

       RtlInitUnicodeString( &DeviceName, EventDrv_NT_DEVICE_NAME );

       //
       // Create the Device object
       //
       Status = IoCreateDevice(
                              DriverObject,
                              0,
                              &DeviceName,
                              FILE_DEVICE_UNKNOWN,
                              0,
                              FALSE,
                              &EventDrvDeviceObject);

       if (!NT_SUCCESS(Status)) {
           return Status;
       }

       RtlInitUnicodeString( &LinkName, EventDrv_WIN32_DEVICE_NAME );
       Status = IoCreateSymbolicLink( &LinkName, &DeviceName );

       if ( !NT_SUCCESS( Status )) {
           IoDeleteDevice( EventDrvDeviceObject );
           return Status;
       }

    //
    // Choose a buffering mechanism
    //
    EventDrvDeviceObject->Flags |= DO_BUFFERED_IO;

    //
    // Register with ETW
    //
    EventRegisterSample_Driver();

    //
    // Log an Event with :  DeviceNameLength
    //                      DeviceName
    //                      Status
    //

    // Copy the device name into the WCHAR local buffer in order
    // to place a NULL character at the end, since this field is
    // defined in the manifest as a NULL-terminated string

    if (DeviceName.Length <= 128 * sizeof(WCHAR)) {

        LengthToCopy = DeviceName.Length;

    }

    RtlCopyMemory(DeviceNameString,
                  DeviceName.Buffer,
                  LengthToCopy);

    DeviceNameString[LengthToCopy/sizeof(WCHAR)] = L'\0';

    EventWriteStartEvent(NULL, DeviceName.Length, DeviceNameString, Status);

    return STATUS_SUCCESS;
   }
   ```

将所有**EventWrite \<*event*\> **宏添加到要引发事件的源代码中。 您可以查看 [Eventdrv 示例](/samples/microsoft/windows-driver-samples/eventdrv/) ，以了解如何为驱动程序源代码中的事件调用其他两个宏。

4. 使用生成的标头文件中的**EventUnregister \<*provider*\> **宏注销驱动程序作为事件提供程序。

   将此函数调用置于驱动程序的卸载例程中。 调用**EventUnregister \<*provider*\> **宏后，不应进行跟踪调用。 由于与进程关联的任何回调函数不再有效，因此在卸载进程时无法取消注册事件提供程序会导致错误。

   ```ManagedCPlusPlus
       // DriverUnload function
       // ...
       //

       //  Unregister the driver as an ETW provider
       //
       EventUnregisterSample_Driver();
   ```

## <a name="5-build-the-driver"></a>5. 构建驱动程序

如果已将仪器清单添加到项目中，并且已将消息编译器配置 ( # A0) 属性，则可以使用 Visual Studio 和 MSBuild 生成驱动程序项目或解决方案。

1. 在 Visual Studio 中打开驱动程序解决方案。

2. 通过选择 " **生成解决方案**"，生成菜单中的示例。 有关生成解决方案的详细信息，请参阅 [构建驱动程序](../develop/building-a-driver.md)。

## <a name="6-install-the-manifest"></a>6. 安装清单

你必须在目标系统上安装清单以便事件使用方 (例如，事件日志) 可以找到包含事件元数据的二进制文件的位置。 如果将消息编译器任务添加到步骤3中的驱动程序项目，则会编译检测清单，并在生成驱动程序时生成资源文件。 使用 Windows 事件命令行实用程序 ( # A0) 安装清单。 安装清单的语法如下所示：

**wevtutil.exe im** *drivermanifest*

例如，若要安装 Evntdrv.sys 示例驱动程序的清单，请使用提升的权限打开命令提示符窗口 (以 **管理员身份运行**) 导航到 evntdrv.xml 文件所在的目录，然后输入以下命令：

```c++
Wevtutil.exe im evntdrv.xml
```

跟踪会话完成后，请使用以下语法卸载清单。

**wevtutil.exe um** *drivermanifest*

例如，若要卸载 [Eventdrv 示例](/samples/microsoft/windows-driver-samples/eventdrv/)的清单：

```c++
Wevtutil.exe um evntdrv.xml
```

## <a name="7-test-the-driver-to-verify-etw-support"></a>7. 测试驱动程序以验证 ETW 支持

安装驱动程序。 执行驱动程序以生成跟踪活动。 查看事件查看器中的结果。 您还可以运行 [Tracelog](tracelog.md)，然后运行 [Tracerpt](/windows-server/administration/windows-commands/tracerpt_1)（一种用于处理事件跟踪日志的工具）来控制、收集和查看事件跟踪日志。