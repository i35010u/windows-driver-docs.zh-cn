---
title: 添加事件跟踪到内核模式驱动程序
description: 添加事件跟踪到内核模式驱动程序
ms.assetid: 74fdb4b2-aad1-4d8a-b146-40a92e1fdbb5
keywords:
- 事件跟踪的 Windows WDK，内核模式
- ETW WDK 内核模式
- 内核模式 ETW WDK 软件跟踪
ms.date: 07/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 60ececc26d2f69b0e8cc260657ef29ddf3bcc728
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519242"
---
# <a name="adding-event-tracing-to-kernel-mode-drivers"></a>添加事件跟踪到内核模式驱动程序

本部分介绍如何使用 Windows 事件跟踪 (ETW) 内核模式 API 将事件跟踪添加到内核模式驱动程序。 ETW 内核模式 API 中引入了 Windows Vista 和更早的操作系统中不支持。 使用[WPP 软件跟踪](wpp-software-tracing.md)或[WMI 事件跟踪](https://msdn.microsoft.com/library/windows/hardware/ff566350)如果您的驱动程序需要支持跟踪功能在 Windows 2000 及更高版本。

> [!TIP]
> 若要查看示例代码，演示如何实现 ETW 使用 Windows Driver Kit (WDK) 8.1 和 Visual Studio，请参阅[Eventdrv 示例](https://go.microsoft.com/fwlink/p/?linkid=256109)。

本节内容：

- [工作流-将事件跟踪添加到内核模式驱动程序](#workflow---adding-event-tracing-to-kernel-mode-drivers)

- [1.决定要引发事件以及将其发布的位置的类型](#1-decide-the-type-of-events-to-raise-and-where-to-publish-them)

- [2.创建仪器指令清单，用于定义提供程序、 事件和通道](#2-create-an-instrumentation-manifest-that-defines-the-provider-the-events-and-channels)

- [3.通过使用消息编译器 (Mc.exe) 编译仪器指令清单](#3-compile-the-instrumentation-manifest-by-using-the-message-compiler-mcexe)

- [4.添加生成的代码以引发 （发布） 事件 （注册、 注销，并将事件写入）](#4-add-the-generated-code-to-raise-publish-the-events-register-unregister-and-write-events)

- [5.生成该驱动程序](#5-build-the-driver)

- [6.安装清单](#6-install-the-manifest)

- [7.测试可验证 ETW 支持的驱动程序](#7-test-the-driver-to-verify-etw-support)

## <a name="workflow---adding-event-tracing-to-kernel-mode-drivers"></a>工作流-将事件跟踪添加到内核模式驱动程序

![若要将事件跟踪添加到内核模式驱动程序的过程的概述。](images/etw-km-process.png)

## <a name="1-decide-the-type-of-events-to-raise-and-where-to-publish-them"></a>1.决定要引发事件以及将其发布的位置的类型

在开始编码之前，必须决定哪种类型的事件所需的驱动程序来记录通过事件跟踪 Windows (ETW)。 例如，你可能想要记录可以帮助您诊断问题，您的驱动程序分布式的之后, 的事件或事件，可帮助你在开发您的驱动程序。 通道标识的事件的类型。 一个*通道*是命名的管理员类型的事件流、 操作、 分析或调试面向特定受众，类似于电视频道。 通道将事件从事件提供程序传递到事件日志和事件使用者。 有关通道和事件类型的信息，请参阅[事件日志和 Windows 事件日志中的频道](https://go.microsoft.com/fwlink/p/?linkid=62587)。

在开发期间，将很可能希望中跟踪事件，可帮助你调试代码。 此同一个通道可以在生产代码中，用于帮助解决该驱动程序部署后可能会出现的问题。 您可能还希望可以用来测量性能; 的跟踪事件这些事件可以帮助 IT 专业人员优化服务器性能和可帮助确定网络瓶颈。

## <a name="2-create-an-instrumentation-manifest-that-defines-the-provider-the-events-and-channels"></a>2.创建仪器指令清单，用于定义提供程序、 事件和通道

检测清单是一个 XML 文件，提供了一个提供程序将引发的事件的形式说明。 检测清单标识的事件提供程序、 指定的通道或通道 （最多 8 个） 和说明的事件，并使用事件模板。 此外，检测清单允许用于字符串本地化，以便可以进行本地化的跟踪消息。 事件系统和事件使用者可以使用结构化 XML 数据执行查询和分析在清单中提供。

有关仪器指令清单的信息，请参阅[检测清单 (Windows) 编写](https://docs.microsoft.com/windows/desktop/WES/writing-an-instrumentation-manifest)并[使用 Windows 事件日志 (Windows)](https://docs.microsoft.com/windows/desktop/WES/using-windows-event-log)。

> [!NOTE]
> 尽管可以手动创作仪器指令清单，则应考虑使用包含在 %windowssdkdir%ECManGen.exe 工具\\bin\\x64 %windowssdkdir%\\bin\\x86\\WDK 和 Visual Studio 安装时的文件夹。 %Windowssdkdir%表示 Windows 工具包 WDK 的此版本的安装的目录，例如，c: 路径\\Program Files (x86)\\Windows 工具包\\8.1。 ECManGen.exe 是应用程序可指导您完成从零开始创建一个清单，而不必使用 XML 标记。 需掌握的中的信息[检测清单 (Windows) 编写](https://docs.microsoft.com/windows/desktop/WES/writing-an-instrumentation-manifest)部分并在[EventManifest 架构 (Windows)](https://docs.microsoft.com/windows/desktop/WES/eventmanifestschema-schema)部分可帮助使用工具时。

以下仪器指令清单显示的事件提供程序将使用名称"示例驱动程序。" 请注意此名称不必是驱动程序二进制文件的名称相同。 清单还提供程序和消息和资源文件的路径指定的 GUID。 消息和资源文件让 ETW 知道进行解码和报告的事件所需的资源的位置。 这些路径点移到驱动程序 (.sys) 文件的位置。 必须在目标计算机上的指定目录中安装驱动程序。

该示例使用名为的通道**系统**，类型的事件的通道**管理员**。此通道是在文件中定义 Winmeta.xml 提供 %windowssdkdir%中使用 Windows Driver Kit (WDK)\\包括\\um 目录。 **系统**通道安全系统的服务帐户运行的应用程序。 清单包括描述的事件时它们已发布，以及在其静态和动态内容一起提供的数据类型的事件模板。 此示例清单定义了三个事件： `StartEvent`， `SampleEventA`，和`UnloadEvent`。

除了渠道之外，您可以使用级别和关键字关联的事件。 关键字和级别提供的方法来启用事件，并提供用于筛选时发布事件的机制。 关键字可用于从逻辑上相关的事件分组在一起。 用于指示严重性或详细程度的事件，例如，关键、 错误、 警告或信息性，可以是一个级别。 Winmeta.xml 文件包含预定义的事件属性的值。

当创建的事件负载 （事件消息和数据） 的模板时，必须指定输入和输出类型。 支持的类型的备注部分所述[ **InputType 复杂类型 (Windows)**](https://docs.microsoft.com/windows/desktop/WES/eventmanifestschema-inputtype-complextype)。

```XML
<?xml version=&#39;1.0&#39; encoding=&#39;utf-8&#39; standalone=&#39;yes&#39;?>
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

## <a name="3-compile-the-instrumentation-manifest-by-using-the-message-compiler-mcexe"></a>3.通过使用消息编译器 (Mc.exe) 编译仪器指令清单

[消息编译器 (Mc.exe)](https://docs.microsoft.com/windows/desktop/WES/message-compiler--mc-exe-)必须运行才能编译你的源代码。 消息编译器包含在 Windows Driver Kit (WDK) 中。 消息编译器会创建包含事件提供程序、 事件属性、 通道和事件的定义的标头文件。 你必须将此头文件包括在源代码中。 消息编译器还会生成的资源编译器脚本 (\*.rc) 和资源编译器脚本包括生成的.bin 文件 （二进制资源）。

在两种方法在生成过程的一部分，可以包括此步骤：

- 将消息编译器任务添加到驱动程序项目文件 (如中所示[Eventdrv 示例](https://go.microsoft.com/fwlink/p/?linkid=256109))。

- 若要添加仪器指令清单和可配置的消息编译器属性，请使用 Visual Studio。

**将消息编译器任务添加到项目文件**有关如何在生成过程中纳入消息编译器的示例，查看项目文件[Eventdrv 示例](https://go.microsoft.com/fwlink/p/?linkid=256109)。 在 Eventdrv.vcxproj 文件中，没有**&lt;MessageCompile&gt;** 调用消息编译器的部分。 消息编译器使用清单文件 (evntdrv.xml) 作为输入，生成标头文件 evntdrvEvents.h。 本部分还指定所生成的 RC 文件的路径，并启用内核模式日志记录宏。 可以复制本部分中，并将其添加到驱动程序项目文件 (.vcxproj)。

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

生成 Eventdrv.sys 示例时，Visual Studio 创建的事件跟踪的必要文件。 它还将 evntdrv.xml 清单添加到驱动程序项目的资源文件的列表。 你可以右键单击要查看的消息编译器属性页的清单。

### <a name="using-visual-studio-to-add-the-instrumentation-manifest"></a>使用 Visual Studio 添加检测清单

您可以将仪器指令清单添加到驱动程序项目，然后配置要生成必要的资源和标头文件的消息编译器属性。

### <a name="to-add-the-instrumentation-manifest-to-the-project-using-visual-studio"></a>若要使用 Visual Studio 向项目添加检测清单

1. 在解决方案资源管理器，将添加到驱动程序项目的清单文件。 右键单击**资源文件&gt;添加&gt;现有项**（例如，evntdrv.xml 或 mydriver.man）。

2. 右键单击刚添加的文件，然后使用属性页可以更改到的项类型**MessageCompile**然后单击**应用**。

3. 消息编译器属性将显示。 下**常规**设置，设置以下选项，然后单击**应用**。

    | 常规                                 | 设置       |
    |-----------------------------------------|---------------|
    | **生成内核模式日志记录宏** | **是 (-km)** |
    | **使用输入的基名称**              | **是 (-b)**  |

4. 下**文件选项**，设置以下选项，然后单击**应用**。

    | 文件选项                                    | 设置         |
    |-------------------------------------------------|-----------------|
    | **生成包含计数器的标头文件** | **是**         |
    | **标头文件路径**                            | **$(IntDir)**   |
    | **生成的 RC 和二进制消息文件路径**  | **是**         |
    | **RC 文件路径**                                | **$(IntDir)**   |
    | **生成的文件的基名称**                   | **$ （filename)** |

默认情况下，消息编译器为其生成的文件的基名称中使用输入文件的基名称。 若要指定的基名称，设置**生成文件基名称**(-z) 字段。 在 Eventdr.sys 示例中，基名称设置为*evntdrvEvents* ，使其匹配的标头文件 evntdrvEvents.h，它包括在 evntdrv.c 名称。

> [!NOTE]
> 如果在 Visual Studio 项目中不包括生成的.rc 文件，可能会收到错误消息中找不到安装清单文件的资源。

## <a name="4-add-the-generated-code-to-raise-publish-the-events-register-unregister-and-write-events"></a>4.添加生成的代码以引发 （发布） 事件 （注册、 注销，并将事件写入）

在仪器指令清单，您定义的事件提供程序和事件说明符的名称。 在编译时使用消息编译器仪器指令清单，消息编译器生成的标头文件描述的资源，还定义了宏的事件。 现在，必须将生成的代码添加到您的驱动程序会引发这些事件。

1. 在源代码文件中，包括事件标头文件生成的消息编译器 (MC.exe)。 例如，在[Eventdrv 示例](https://go.microsoft.com/fwlink/p/?linkid=256109)，Evntdrv.c 源文件包括在上一步中生成的标头文件 (evntdrvEvents.h):

   ```c++
   #include "evntdrvEvents.h"  
   ```

2. 添加注册和取消注册为事件提供程序的驱动程序的宏。 例如，在头文件。 [Eventdrv 示例](https://go.microsoft.com/fwlink/p/?linkid=256109)(evntdrvEvents.h)，消息编译器会创建基于提供程序的名称的宏。 在清单中， [Eventdrv 示例](https://go.microsoft.com/fwlink/p/?linkid=256109)使用名称"示例驱动程序"作为提供程序的名称。 消息编译器将提供程序的名称与事件宏注册提供程序，在这种情况下，结合起来**EventRegisterSample\_驱动程序**。

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

   添加**EventRegister\<*提供程序*\>** 宏为你[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)函数。 创建并初始化设备对象的代码后添加此函数。 请注意，必须匹配对的调用**EventRegister\<*提供程序*\>** 函数通过调用**EventUnregister\< *提供程序*\>**。 您可以在您的驱动程序中注销该驱动程序[ </em>*卸载** ](<https://msdn.microsoft.com/library/windows/hardware/ff564886>)例程。

   ```ManagedCPlusPlus
      // DriverEntry function
      // ...


       // Register with ETW
       //
       EventRegisterSample_Driver();
    ```

3. 将生成的代码添加到您的驱动程序的源代码文件，以编写 （引发） 事件清单中所指定。 从清单编译的标头文件包含的驱动程序生成的代码。 使用**EventWrite\<*事件*\>** 在要发布到 ETW 的跟踪消息的标头文件中定义的函数。 例如，下面的代码显示了事件为 evntdrvEvents.h 中定义的宏[Eventdrv 示例](https://go.microsoft.com/fwlink/p/?linkid=256109)。

   宏将这些事件写入称为： `EventWriteStartEvent`， `EventWriteSampleEventA`，和`EventWriteUnloadEvent`。 您可以看到这些宏的定义中，会自动包括宏定义**EventEnabled\<*事件*\>** 检查事件是否启用了宏。 检查无需生成负载，如果未启用该事件。

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

   添加**EventWrite\<*事件*\>** 宏插入源代码中所引发的事件。 例如，下面的代码片段演示[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/wdf/driverentry-for-kmdf-drivers)从日常[Eventdrv 示例](https://go.microsoft.com/fwlink/p/?linkid=256109)。 *DriverEntry*包括宏来向 ETW 注册驱动程序 (*EventRegisterSample\_驱动程序*) 以及将驱动程序事件写入 ETW 的宏 (*EventWriteStartEvent*)。

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

    DeviceNameString[LengthToCopy/sizeof(WCHAR)] = L&#39;\0&#39;;

    EventWriteStartEvent(NULL, DeviceName.Length, DeviceNameString, Status);

    return STATUS_SUCCESS;
   }
   ```

添加的所有**EventWrite\<*事件*\>** 宏插入源代码中所引发的事件。 你可以检查[Eventdrv 示例](https://go.microsoft.com/fwlink/p/?linkid=256109)若要查看其他两个宏的驱动程序源代码中的事件的调用方式。

4. 取消驱动程序注册为事件提供程序使用**EventUnregister\<*提供程序*\>** 宏生成的头文件中。

   将此函数调用放在您的驱动程序卸载例程。 不跟踪调用应进行后**EventUnregister\<*提供程序*\>** 宏调用。 若要取消注册事件提供程序都可能导致错误时该过程将被卸载，因为与进程关联的任何回调函数都不再有效。

   ```ManagedCPlusPlus
       // DriverUnload function
       // ...
       //

       //  Unregister the driver as an ETW provider
       //
       EventUnregisterSample_Driver();
   ```

## <a name="5-build-the-driver"></a>5.生成驱动程序

如果您已添加到项目中检测清单，并配置消息编译器 (MC.exe) 属性，可以生成的驱动程序项目或使用 Visual Studio 和 MSBuild 的解决方案。

1. 在 Visual Studio 中打开驱动程序解决方案。

2. 通过选择生成该示例从生成菜单**生成解决方案**。 有关构建解决方案的详细信息，请参阅[构建一个驱动程序](https://docs.microsoft.com/windows-hardware/drivers/develop/building-a-driver)。

## <a name="6-install-the-manifest"></a>6.安装清单

您必须在目标系统上安装清单，以便事件使用者 （例如，事件日志） 可以包含事件元数据的二进制文件的位置。 如果消息编译器任务添加到步骤 3 中的驱动程序项目中时，检测清单已经过编译，生成该驱动程序时生成的资源文件。 使用 Windows 事件命令行实用程序 (Wevtutil.exe) 安装清单。 若要安装清单的语法如下所示：

**wevtutil.exe im** *drivermanifest*

例如，若要安装 Evntdrv.sys 示例驱动程序的清单，请打开命令提示符窗口使用提升的权限 (**以管理员身份运行**) 导航到 evntdrv.xml 文件所在的目录并输入以下命令：

```c++
Wevtutil.exe im evntdrv.xml
```

跟踪会话完成后，卸载使用以下语法在清单。

**wevtutil.exe um** *drivermanifest*

例如，若要卸载的清单[Eventdrv 示例](https://go.microsoft.com/fwlink/p/?linkid=256109):

```c++
Wevtutil.exe um evntdrv.xml
```

## <a name="7-test-the-driver-to-verify-etw-support"></a>7.测试可验证 ETW 支持的驱动程序

安装驱动程序。 练习要生成的跟踪活动的驱动程序。 在事件查看器中查看结果。 您还可以运行[Tracelog](tracelog.md)，然后运行[Tracerpt](https://docs.microsoft.com/windows-server/administration/windows-commands/tracerpt_1)、 一个工具，用于处理事件跟踪日志、 控制、 收集和查看事件跟踪日志。
